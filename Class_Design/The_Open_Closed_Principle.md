### 2.1
```py
class GenericEncoder:

    def encode_to_format(self, data, format) -> str:
        if format == "json":
            encoder = JsonEncoder()
        elif format == "xml":
            encoder = XmlEncoder()
        else:
            raise InvalidArgumentException("Unknown format")

        data = self._prepare_data(data, format)

        return encoder.encode(data)
```

### 2.2
```py
class GenericEncoder:

    def encode_to_format(self, data, format) -> str:
        if format == "json":
            encoder = JsonEncoder()
        elif format == "xml":
            encoder = XmlEncoder()
        elif format == "yaml":
            encoder = YamlEncoder()
        else:
            raise InvalidArgumentException("Unknown format")

        data = self._prepare_data(data, format)

        return encoder.encode(data)
```

### 2.3
```py
class GenericEncoder:

    def encode_to_format(self, data, format) -> str:
        if format == "json":
            encoder = JsonEncoder()
        elif format == "xml":
            encoder = XmlEncoder()
        else:
            raise InvalidArgumentException("Unknown format")

        data = self._prepare_data(data, format)

        return encoder.encode(data)

    def _prepare_data(self, data, format):
        switch format:
            case "json":
                data = self.force_array(data)
                data = self.fix_keys(data)
            case "xml":
                data = self.fix_attributes(data)
            case "_"
                raise InvalidArgumentException("Format not supported")
        return data
```

### 2.4
```py
from abc import ABC, abstractmethod

class EncoderInterface(ABC):

    @abstractmethod
    def encode(data) -> str:
        pass

class JsonEncoder(EncoderInterface):
    
    def encode(data) -> str:
        pass

class XmlEncoder(EncoderInterface):
    
    def encode(data) -> str:
        pass

class YamlEncoder(EncoderInterface):
    
    def encode(data) -> str:
        pass
```

### 2.5
```py
class EncoderFactory:

    def create_for_format(self, format) -> EncoderInterface:
        if format == "json":
            return JsonEncoder()
        elif format == "xml":
            return XmlEncoder()
        elif format == "yaml":
            return YamlEncoder()
        raise InvalidArgumentException("Unknown format")
```

### 2.6
```py
class GenericEncoder:
    _encoder_factory = None

    def __init__(self, encoder_factory: EncoderFactory):
        self._encoder_factory = encoder_factory

    def encode_to_format(self, data, format) -> str:
        encoder = self._encoder_factory.create_for_format(format)
        data = self._prepare_data(data, format)
        return encoder.encode(data)
```

### 2.7
```py
class EncoderFactoryInterface(ABC):

    @abstractmethod
    def create_for_format(self, format) -> EncoderInterface:
        pass


class EncoderFactory(EncoderFactoryInterface):

    def create_for_format(self, format) -> EncoderInterface:
        if format == "json":
            return JsonEncoder()
        elif format == "xml":
            return XmlEncoder()
        elif format == "yaml":
            return YamlEncoder()
        raise InvalidArgumentException("Unknown format")



class GenericEncoder:
    _encoder_factory = None

    def __init__(self, encoder_factory: EncoderFactoryInterface):
        self._encoder_factory = encoder_factory

    def encode_to_format(self, data, format) -> str:
        encoder = self._encoder_factory.create_for_format(format)
        data = self._prepare_data(data, format)
        return encoder.encode(data)        

    def _prepare_data(self, data, format):
        switch format:
            case "json":
                data = self.force_array(data)
                data = self.fix_keys(data)
            case "xml":
                data = self.fix_attributes(data)
            case "_"
                raise InvalidArgumentException("Format not supported")
        return data
```

### 2.8
```py
class MyCustomEncoderFactory(EncoderFactoryInterface):

    def create_for_format(self) -> EncoderInterface:
        pass

encoder = GenericEncoder(MyCustomEncoderFactory())
```
