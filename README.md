# Book Search Engine Starter Code

# Weather-Dashboard

## Table of contents

- [Overview](#overview)
  - [Description](#description)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
- [Author](#author)

## Overview

### Description

- This application is used for searching for books using the Google books API. A user login and sign-up, search for books, and save them to their favorites list as well as removing them.

### The challenge

Users should be able to:

- search books and save at list
- login and sign-up
- delete saved book in list

### Screenshot

![](./client/assets/images/Google%20Book%20Search1.png)
![](./client/assets/images/Google%20Book%20Search2.png)
![](./client/assets/images/Google%20Book%20Search3.png)

### Links

- Solution URL: [https://github.com/YangLongWang/Book-Search-Engine](https://github.com/YangLongWang/Book-Search-Engine)
- Live Site URL: [https://search-book-app-6408.herokuapp.com/](https://search-book-app-6408.herokuapp.com/)

## My process

### Build with

- HTML
- CSS
- JAVASCRIPT

### What I learned

- setting Graphql

To see how I add code snippets, see below:

```Javascript
const typeDefs = gql`
  type User {
    _id: ID
    username: String
    email: String
    bookCount: Int
    savedBooks: [Book]
  }

  type Book {
    bookId: String
    authors: [String]
    description: String
    image: String
    title: String
    link: String
  }

  type Query {
    me: User
  }

  type Auth {
    token: ID!
    user: User
  }

  type Mutation {
    loginUser(email: String!, password: String!): Auth
    addUser(username: String!, email: String!, password: String!): Auth
    saveBook(
      bookId: String
      authors: [String]
      description: String
      title: String
      image: String
      link: String
    ): User
    removeBook(bookId: ID!): User
  }
`;

Query: {
  me: async (parent, args, context) => {
    if (context.user) {
      const userData = await User.findOne({ _id: context.user._id }).select(
        "-__v -password"
      );

      return userData;
    }

    throw new AuthenticationError("Not logged in");
  },
},
Mutation: {
  addUser: async (parent, args) => {
    const user = await User.create(args);
    const token = signToken(user);

    return { token, user };
  },
}
```

## Author

- Github - [Longyang Wang](https://github.com/YangLongWang)
