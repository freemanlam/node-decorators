# Socket#3.2.0
* Made global middleware optional
* Made dependencies as peerDependencies

# Socket#3.1.0
* Changed library structure
* Fixed interfaces
* Added new interface to implement for server middleware `ServerMiddleware`, controller `Middleware` interface remains the same
* Updated versions of dependencies, like `socket.io` and `@decorators/di`

# Socket#3.0.2
* Fix sorting parameters when applying events

# Socket#3.0.1
* Updated README

# Socket#3.0.0
* Dependency injection with `@decorators/di`
* `@ServerMiddleware` decorator was removed, use `IO_MIDDLEWARE` token to register custom server middleware
* `@Middleware` decorator was removed use controller-based middleware
* Middlewares as a class
* Functions as middleware are no longer supported, use classes instead (`Middleware` interface)
* Single middleware are no longer supported, use array instead (unified interface for all usages)
* legacy helper function `attachControllersToSocket` was removed
* Updated `socket.io` version to `>=2.0.4`
* Development: big refactoring
* Development: updated typescript version to `>=2.6.1`

# Socket#2.0.1
* Fixed availability of **@Socket** in `connection` event
* Updated typescript to latest
* Fixed types for latest typescript

# Socket#2.0.0
* Features
  * Added wrap option for **@IO(WrapperClass?)** decorator, see **@Socket()** decorator for details
* Renamed
  * **@Callback()** to **@Ack()**
  * **@GlobalMiddleware()** for socket global middleware to **@Middleware()**
  * Renamed **@Namespace()** to **@Controller(namespace: string, middleware?: Function | Function[])**
* Removed
  * **@Middleware(middleware: Function | Function[])** - use Controller based middleware
  * deprecated **bootstrapSocketIO(io: SocketIO.Server, Controllers)** -  Attaches controllers to IO server - use **attachControllers()** instead
  * deprecated **attachControllerToSocket(io: SocketIO.Server, socket: SocketIO.Socket, Controllers)** -  Attaches controllers to Socket - use **attachControllersToSocket()** instead

# Socket#1.4.0
* Controller DI
```typescript
{ provide: UserController, deps: [UserService] }
```
* Renamed methods **bootstrapSocketIO** and **attachControllerToSocket** (see README for details)

# Socket#1.3.3
* Added possibility to pass array of middleware funcs into:
   * **@ServerMiddleware**
   * **@GlobalMiddleware**
   * **@Middleware**

# Socket#1.3.2
* Added wrap option for **@Socket(WrapperClass?)** decorator, now you can pass wrapper class in it, to get extended functionality over the socket, optional parameter, e.g.:
```typescript
class SocketWrapper {
  constructor(private socket: SocketIO.Socket) {}
}
```

# Socket#1.3.1
* Added callback function (noop) even if it doesn't exists, just prevent additional checks in controller

# Socket#1.3.0
* Renamed middleware names to
   * **@ServerMiddleware**
   * **@GlobalMiddleware**
   * **@Middleware**
* Renamed decorators:
   * **@Namespace**
   * **@GlobalEvent**
   * **@Connection**
   * **@Disconnect**
   * **@Event**
* Added event-based middleware, for socket events

# Socket#1.2.2
* Automatic definitions generation

# Socket#1.2.1
* added new parameters to middleware functions:
  * **@Middleware((io: SocketIO.Server | SocketIO.Namespace, socket: SocketIO.Socket, next: Function) => {})** - registers global (io) middleware
  * **@SocketMiddleware((io: SocketIO.Server | SocketIO.Namespace, socket: SocketIO.Socket, packet, next: Function) => {})** - registers socket middleware

# Socket#1.2.0
* Updated Socket.io version to **1.6.0**
* Removed **attachController** for the sake of **attachControllers**
* **bootstrapSocketIO** now accepts io server instance as first argument and array of controllers as second
* New **@Controller(namespace: string)** decorator, registers namespace for sockets
* **attachControllerToSocket(io: SocketIO.Server, socket: SocketIO.Socket, Controllers)** -  Attaches controllers to Socket

# Socket#1.1.2
* Moved server configuration out of **@Connect** decorator to **bootstrapSocketIO**
  ```
  bootstrapSocketIO(httpServerInstance || 3000)
  ```
* Removed  **@Connect** decorator
* **attachControllers** attach array of controllers

# Socket#1.1.1
* new socket.io decorator
  ##### Method
    * **@OnDisconnect()**
* **SocketIOServer** interface added
  * **attachController** will now return correct object (SocketIOServer, this)

# Socket#1.1.0
* New socket.io decorators
  #### Functions
  * **bootstrapSocketIO(rootController: Controller)**
  ##### Class
  * **@Connect(serverOrPort: number | string | HttpServer, opts?: any)**
  * **@Middleware(fn: Function)**
  ##### Method
  * **@OnIO(event: string)**
  * **@OnConnect()**
  * **@OnConnection()**
  * **@OnSocket(event: string)**
  ##### Parameter
  * **@IO()**
  * **@Socket()**
  * **@Args()**
  * **@Callback()**
