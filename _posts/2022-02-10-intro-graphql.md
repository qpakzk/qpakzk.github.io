---
layout: post
title: "Github GraphQL API로 GraphQL 이해하기"
description: "GraphQL 시리즈 1편"
tags: [GraphQL]
redirect_from:
  - /2022/02/10/
---

# Github GraphQL API로 GraphQL 이해하기

GraphQL은 페이스북에서 개발한 API를 위한 쿼리 언어(query language)이다.
GraphQL를 활용한 공개 API로 Github GraphQL API가 있는데, 이를 통해 GraphQL을 살펴보도록 하겠다.
2022년 2월 11일 기준 [Github GraphQL API Explorer](https://docs.github.com/en/graphql/overview/explorer)에 접속하여 Github GraphQL API를 사용해볼 수 있다.

| ![GraphQL API Explorer](/assets/images/graphql/intro-graphql/graphql-explorer.png) |
|:--:|
| Image 1. GraphQL API Explorer |

GraphQL은 스키마를 인터페이스로 통신하기 때문에 스키마가 정의되어야 한다.
Documentation Explorer를 통해 Github에서 정의한 스키마를 확인할 수 있다.
GraphQL 스키마는 Query와 Mutation에서 시작한다. CRUD 연산에서 Query는 데이터 조회(R), Mutation은 데이터 조작(CUD)을 담당한다.


## Query

Documentation Explorer에서 Query를 클릭하면, Query에 정의된 필드들을 확인할 수 있다.
필드 마다 리졸버(resolver)가 있어서 이를 통해 필드 타입에 맞는 값을 응답해준다.

Query로 리눅스 커널 레포지토리를 조회해보자.
Query 필드 중에 `repository`가 있는데 정의는 다음과 같다.

```graphql
repository(
followRenames: Boolean = true
name: String!
owner: String!
): Repository
```

`repository`는 인자(argument)로 `followRenames`, `name`, `owner`를 입력하면 `Repository` 타입에 맞는 데이터를 반환해준다.
참고로 `name`, `owner`의 타입인 String 뒤에 `!`가 붙어있는데 이는 필수값(not null)을 의미한다.
리눅스 커널 레포지토리를 조회하기 위해 `name`에 레포지토리명인 `linux`, `owner`에 Github 계정명인 `torvalds`를 입력한다.

`repository`의 응답 타입인 `Repository`에도 많은 필드들이 정의되어 있다.
GraphQL의 장점은 클라이언트가 `Repository` 필드 중에서 원하는 필드만 열거하여 조회할 수 있다는 것이다.
리눅스 커널에서 레포지토리 id, 설명, fork 횟수, star 횟수를 조회해보도록 하겠다.

```graphql
query {
  repository(name:"linux", owner: "torvalds") {
    id
    description
    forkCount
    stargazerCount
  }
}
```

결과는 다음과 같다.

| ![GraphQL Query](/assets/images/graphql/intro-graphql/query.png) |
|:--:|
| Image 2. GraphQL Query |

실제로 리눅스 커널 레포지토리에 접속해보면 결과가 동일하다는 것을 확인할 수 있다.

| ![Linux Kernel Repository](/assets/images/graphql/intro-graphql/linux.png) |
|:--:|
| Image 3. Linux Kernel Repository |

## Mutation

Query와 마찬가지로 Documentation Explorer에서 Mutation을 클릭하면, Mutation에 정의된 필드들을 확인할 수 있다.
Mutation으로 새로운 레포지토리를 생성해보자.
Mutation 필드 중에 `createRepository`를 통해 새로운 레포지토리를 생성할 수 있는데 정의는 다음과 같다.

```graphql
createRepository(input: CreateRepositoryInput!): CreateRepositoryPayload
```

`createRepository`는 인자(argument)로 `CreateRepositoryInput` 타입의 `input`을 입력받고, `CreateRepositoryPayload` 타입의 데이터를 반환해준다.
`input`을 입력할 때 필수값 이외에 저장하고 싶은 필드들을 입력해주면 된다.
응답 또한 `CreateRepositoryPayload` 타입에서 응답받고 싶은 필드를 열거하면 된다.

```graphql
mutation {
  createRepository(input: {
    name: "hola-mundo",
    description: "This is an example repository.",
    visibility: PRIVATE
  }) {
    clientMutationId
    repository {
      id
      description
    }
  }
}
```

결과는 다음과 같다.

| ![GraphQL Mutation](/assets/images/graphql/intro-graphql/mutation.png) |
|:--:|
| Image 4. GraphQL Mutation |

실제로 `hola-mundo`라는 이름의 프라이빗 레포지토리가 생성된 것을 확인할 수 있다.

| ![hola-mundo](/assets/images/graphql/intro-graphql/hola-mundo.png) |
|:--:|
| Image 5. hola-mundo Repository |

## Conclusion

Github GraphQL API를 통해 GraphQL에 대해 직관적으로 파악해보았다.
다음 포스트에서는 GraphQL 특징 및 구조에 대해 살펴보도록 하겠다.
