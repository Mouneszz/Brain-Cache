### What is Socket.IO?

**Socket.IO** is a library that enables real-time, bi-directional communication between the client (browser) and the server.  
It uses WebSockets under the hood (with fallbacks like long polling) and is commonly used in **chat apps**, **notifications**, **live updates**, etc.

### 🧱 Core Components in Flask Chat App

#### 1. **Initialization**

Set up Socket.IO with Flask:
```python
from flask_socketio import SocketIO

app = Flask(__name__)
socketio = SocketIO(app)
```
`SocketIO(app)` wraps the Flask app and enables real-time WebSocket communication.

#### 2. **Sending Messages (Client → Server)**
The client sends a message using:
```javascript
socket.send("Hello, world!");
```
The server listens with:
```js
@socketio.on("message")
def handle_message(msg):
    print("Received:", msg)
    send(msg, broadcast=True)
```

**Definitions**:
- `@socketio.on("message")`: Decorator to handle "message" events.
- `msg`: The actual message content sent from the client.
- `send(msg, broadcast=True)`: Sends the message to **all** connected clients.

#### 3. **Receiving Messages (Server → Client)**
The client listens for incoming messages:
```javascript
socket.on("message", function(msg) {
    // Display message in the chat window
});
```
📝 **Definition**:
- `socket.on("message", callback)`: Receives the server's broadcast and executes the callback with the message.

### Flow of a Chat Message
1. **User types a message** in chat box.
2. **Client emits the message** using `socket.send(msg)`.
3. **Server receives and rebroadcasts** to all clients using `send(msg, broadcast=True)`.
4. **Each client receives the message** using `socket.on("message", ...)`.
5. **Client-side JavaScript** appends message to the DOM (chat window).

