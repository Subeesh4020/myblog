# MyBlog — Full-Stack Social Media Platform

## Project Overview

MyBlog is a full-stack social media platform designed to allow users to create, share, and interact with posts while connecting with other users.

The project is built using a modern multi-service architecture, combining JavaScript/TypeScript, Rust, Elixir, and Python to explore different technologies and their practical use in a real-world application.

The platform includes user authentication, post creation, likes and dislikes, nested comments, user relationships, personalized feeds, real-time chat, notifications, and AI-powered content moderation.

The main goal of this project is to build a complete social media application while learning how modern backend systems, distributed services, caching, messaging, and AI components work together.


## Project Explanation
What is MyBlog?

MyBlog is a social media application where users can create posts and interact with content shared by other users.

Users can:

<li> Create and share posts.

<li> Like and dislike posts and comments.

<li> Write comments and reply to other comments.

<li> Follow other users.

<li> View a personalized feed.

<li> Chat with other users in real time.

<li> Receive notifications.

<li> Manage their profiles and relationships. <br>

The application is designed to demonstrate how a social media platform can be developed using multiple backend services instead of relying on a single backend application.

## Main Architecture

The project follows a multi-service backend architecture.

Different services are responsible for different tasks, such as API handling, fast data fetching, real-time communication, and AI processing.

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


## Technology Stack
<li> Layer
<li> Technologies
<li> Frontend
    <li> React, TypeScript, Vite, CSS Modules
<li> Main Backend
    <li> Node.js, Express, TypeScript
<li> Database
    <li> MongoDB, Mongoose, MongoDB Atlas
<li> Fast Data API
    <li> Rust, Axum
<li> Real-Time Chat
    <li> Elixir, Phoenix, WebSockets
<li> AI Service
    <li> Python, Hugging Face models
<li> Messaging
    <li> Kafka
<li> Caching
    <li> Redis / Valkey
<li> Background Jobs
    <li> BullMQ
<li> Containerization
    <li> Podman / Docker
