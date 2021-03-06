## About

```python
class ServerManager():
	"""
	Functions for managing IP-addresses. Intended to be used as a mixin for CloudManager.
	"""
```

`ServerManager` is a mixed into `CloudManager` and the following methods are available by

```python
manager = CloudManager("api-username", "password")
manager.method()
```

## Methods


```python
def get_servers(self, populate=False):
	"""
	Returns a list of (populated or unpopulated) Server instances. 
	Populate = False (default) => 1 API request, returns unpopulated Server instances.
	Populate = True => Does 1 + n API requests (n = # of servers), returns populated Server instances.
	"""
```

```python
def get_server(self, UUID):
	"""
	Returns a (populated) Server instance.
	"""
```

```python
def create_server(self, server):
	"""
	Creates a server and its storages based on a (locally created) Server object. 
	Populates the given Server instance with the API response.

	Example:
	server1 = Server( core_number = 1,
				memory_amount = 512, 
				hostname = "my.example.1", 
				zone = ZONE.London, 
				storage_devices = [
					Storage(os = "Ubuntu 14.04", size=10, tier=maxiops, title='The OS drive'),
					Storage(size=10),
					Storage()
				title = "My Example Server"
			])
	manager.create_server(server1)

	One storage should contain an OS. Otherwise storage fields are optional.
	- size defaults to 10,
	- title defaults to hostname + " OS disk" and hostname + " storage disk id" (id is a running starting from 1)
	- tier defaults to maxiops
	- valid operating systems are: 
		"CentOS 6.5", "CentOS 7.0"
		"Debian 7.8"
		"Ubuntu 12.04", "Ubuntu 14.04"
		"Windows 2003","Windows 2008" ,"Windows 2012"

	"""
```

```python
def modify_server(self, UUID, **kwargs):
	"""
	modify_server allows updating the server's updateable_fields.
	Note: Server's IP-addresses and Storages are managed by their own add/remove methods.
	"""
```

```python
def delete_server(self, UUID):
	"""
	DELETE '/server/UUID'. Permanently destroys the virtual machine. 
	DOES NOT remove the storage disks.

	Returns an empty object.
	"""
```

```python
def get_server_data(self, UUID):
	"""
	Returns '/server/uuid' data in Python dict. 
	Creates object representations of any IP-address and Storage.
	"""
```