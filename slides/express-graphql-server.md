---
layout: slides
---

<section>
    <h1>Express GraphQL Server</h1>
</section>

<section>
    <h2>GraphQL Types</h2>
    <ul>
        <li>String</li>
        <li>Int</li>
        <li>Float</li>
        <li>Boolean</li>
        <li>ID</li>
        <li>Query</li>
        <li>Mutation</li>
        <li>???</li>
    </ul>
</section>

<section>
    <section>
        <h2>Query Type</h2>
    </section>

    <section>
        <pre>
<code class="hljs" data-line-numbers="">
const typeDefs = `
    type Query {
    greeting: String!
    }
`;
</code>
        </pre>
    </section>
</section>

<section>
    <section>
        <h2>Mutation Type</h2>
    </section>

    <section>
        <pre>
<code class="hljs" data-line-numbers="">
const typeDefs = `
type Mutation {
    setGreetingMessage(message: String!): String 
    }
`;
</code>
        </pre>
    </section>
</section>

<section>
    <section>
        <h2>Resolvers</h2>
    </section>

    <section>
        <pre>
<code class="hljs" data-line-numbers="">
let greetingMsg = "Hello, world!";
</code>
        </pre>
    </section>
    <section>
            <pre>
<code class="hljs" data-line-numbers="">
const resolvers = {
    Query: {
        greeting () => greetingMsg;
    }
},
</code>
            </pre>
    </section>
    <section>
                <pre>
<code class="hljs">
Mutation: {
    setGreetingMessage
}
</code>
                </pre>
            </section>
            <section>
                    <pre>
<code class="hljs">
function setGreetingMessage(_, { message }) {
    return greetingMsg = message;
}
</code>
                    </pre>
                </section>
                <section>
                        <pre>
<code class="hljs" data-line-numbers="">
function(obj, args, context, info)
</code>
                        </pre>
                    </section>
</section>

<section>
    <section>
        <h2>Express/Apollo Server</h2>
    </section>

    <section>
        <pre>
<code class="hljs" data-line-numbers="">
const express = require('express');
const { ApolloServer } = require('apollo-server-express');

// import typeDefs and reslovers or define here...

const app = express();

const server = new ApolloServer({
    typeDefs,
    resolvers,
});

server.applyMiddleware({ app, path: '/graphql' });

app.listen(3000, function () {
    console.log('App Started on port 3000);
});
</code>
        </pre>
    </section>
</section>

<section>
    <h1>DEMO</h1>
    <a href="https://repl.it/@yourwebdevguy/backend-nodejs-server-demo">https://repl.it/@yourwebdevguy/backend-nodejs-server-demo</a>
</section>

<section>
    <h1>Thank You!</h1>
</section>