# graphql-server-apollo-example

I've created an example of a GraphQL server using Apollo GraphQL server. I hope it can be useful to someone who is learning GraphQL with Apollo.
https://www.apollographql.com/docs/apollo-server/

## Install dependencies
```
npm install
```

## Run the example
```
node index.js
```

## Deploying using Glitch
You can run the server code in glitch. It has been tested to be working fine. You can fork the repository in your github account and import the repo in glitch. Glitch is free hosting for nodejs code.


## Here is the full code in this example:
```
const { ApolloServer, gql } = require('apollo-server');

const typeDefs = gql`
  type Job {
    id: Int
    position: String
    company: String
    description: String
    location: String
    employmentType: String
    skillsRequired: [String]
  }

  type Query {
    job(id: Int!): [Job],
    jobs: [Job]
  }
`;

const jobs = [
  {
    id: 1,
    position: 'Software Engineer',
    company: 'Apple',
    description: 'job description',
    skillsRequired: ['Go', 'GraphQL'],
    location: 'location',
    employmentType: 'full-time',
  },
  {
    id: 2,
    position: 'Software Engineering Manager',
    company: 'Google',
    description: 'job description',
    skillsRequired: ['Scrum', 'JIRA'],
    location: 'location',
    employmentType: 'full-time',
  },
  {
    id: 3,
    position: 'System Engineer',
    company: 'Microsoft',
    description: 'job description',
    skillsRequired: ['Linux', 'Kubernetes'],
    location: 'location',
    employmentType: 'full-time',
  },
  {
    id: 4,
    position: 'Frontend Engineer',
    company: 'Facebook',
    description: 'job description',
    skillsRequired: ['React', 'GraphQL'],
    location: 'location',
    employmentType: 'full-time',
  },
];

var queryJobs = (jobId) => {
  return jobs.filter((job, index, filteredArray) => {
        return job.id == jobId
  });
}

const resolvers = {
  Query: {    
    //Reference: https://www.apollographql.com/docs/graphql-tools/resolvers/
    job: (parent, args, context, info) => {
      return queryJobs(args.id) 
    },
    jobs: () => jobs
  },
};

const server = new ApolloServer({ typeDefs, resolvers });

server.listen().then(({ url }) => {
  console.log(`🚀  Server ready at ${url}`);
});
```

Visit my blog http://www.melvinvivas.com for more tech articles



