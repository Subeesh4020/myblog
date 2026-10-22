# Main Architecture

The project follows a multi-service backend architecture.

Different services are responsible for different tasks, such as API handling, fast data fetching, real-time communication, and AI processing.
```  
                         MyBlog
                           |
                    React Frontend
                           |
                    API Communication
                           |
                    Node.js / Express
                           |
        ┌──────────────────┼──────────────────┐
        |                  |                  |
     MongoDB             Kafka             Redis
        |                  |                  |
   Persistent         Event Messaging    Cache / Queues
     Storage               |                  |
                           |
                 ┌─────────┴─────────┐
                 |                   |
             Python AI          Other Services
             Moderation

        Rust Axum API       Elixir Phoenix Chat
```
