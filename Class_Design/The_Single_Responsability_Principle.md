### 1.1
```py
class ConfirmationMailMailer:
    def __init__(
        self,
        templating: TemplatingEngineInterface,
        translator: TranslatorInterface,
        mailer: MailerInterface,
    ):
        self._templating = templating
        self._translator = translator
        self._mailer = mailer

    def send_to(self, user):
        message = self._create_message_for(user)
        self._send_message(message)

    def _create_message_for(self, user) -> Message:
        subject = self._translator.translate("Confirm your mail address")
        body = self._templating.render(
            "confirmationMail.html.tpl",
            {"confirmation_code": user.get_confirmation_code()},
        )
        message = Message(subject, body)
        message.set_to(user.get_email_address())
        return message

    def _send_message(self, message):
        self._mailer.send(message)
```

### 1.2
```py
class ConfirmationMailMailer:
    def __init__(
        self, confirmation_mail_factory: ConfirmationMailMailer, mailer: MailerInterface
    ):
        _confirmation_mail_factory = confirmation_mail_factory
        _mailer = mailer

    def send_to(self, user):
        message = self.create_message_for(user)
        self.send_message(message)

    def _create_message_for(self, user) -> Message:
        return self._confirmation_mail_factory.create_message_for(user)

    def _send_message(self, message: Message):
        return self._mailer.send(message)


class ConfirmationMailFactory:
    def __init__(
        self, templating: TemplatingEngineInterface, translator: TranslatorInterface
    ):
        _templating = templating
        _translator: translator

    def create_message_for(self, user):
        subject = self._translator.translate("Confirm your mail address")
        body = self._templating.render(
            "confirmationMail.html.tpl",
            {"confirmation_code": user.get_confirmation_code()},
        )
        message = Message(subject, body)
        message.set_to(user.get_email_address())
        return message
```

## Classes needed to understand the previous examples

```py
from abc import ABC, abstractmethod

class TemplatingEngineInterface(ABC):
    @abstractmethod
    def render(self):
        pass


class TranslatorInterface(ABC):
    @abstractmethod
    def translate(self, message):
        pass


class MailerInterface(ABC):
    @abstractmethod
    def send(self):
        pass


class Message:
    def __init__(self, subject, body):
        self.subject = subject
        self.body = body

    def set_to(self, user):
        pass

```
