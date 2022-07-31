### 3.1
```py
class ConcretClass:

	def implemented_method(self):
		pass
```

```py
from abc import ABC, abstractmethod

class AbstractClass(ABC):

	@abstractmethod
	def abstract_method(self):
		pass

	def implemented_method(self):
		pass
```

```py
from abc import ABC, abstracmethod

class AnInterface(ABC):
	
	@abstractmethod
	def abstract_method(self):
		pass
```

### 3.2
```py
from abc import ABC, abstractmethod

class FileInterface(ABC):

	@abstractmethod
	def rename(self, name: str) -> None:
		pass

	@abstractmethod
	def change_owner(self, user: str, group:str) -> None:
		pass
```

### 3.3
```py
class DropboxFile(FileInterface):

	def rename(self, name:str) -> None:
		pass

	def change_owner(self, user:str, group:str) -> None:
		raise BadMethodCallException("Not implemented for Dropbox files")
```

### 3.4
```py
if not isinstance(file, DropboxFile):
	file.change_owner("user", "group");
```

### 3.5
```py
class DropboxFile(FileInterface):
	
	def change_owner(self, user:str, group:str) -> None:
		pass 
```

### 3.6
```py
from abc import ABC, abstractmethod

class FileInterface(ABC):
	
	@abstractmethod
	def rename(self, name:str) -> None:
		pass


class FileWithOwnerInterface(FileInterface):

	@abstractmethod
	def change_owner(self, user: str, group: str) -> None:
		pass
```

### 3.7
```py
class DropboxFile(FileInterface):

	def rename(self, name:str) -> None:
		pass
```

### 3.8
```py
class LocalFile(FilewithOwnerInterface):

	def change_name(self, name:str) -> None:
		pass

	def change_owner(self, user:str, group:str) -> None:
		pass
```
