**PROTOCOL**

# `ApolloClientProtocol`

```swift
public protocol ApolloClientProtocol: class
```

> The `ApolloClientProtocol` provides the core API for Apollo. This API provides methods to fetch and watch queries, and to perform mutations.

## Properties
### `store`

```swift
var store: ApolloStore
```

> A store used as a local cache.

### `cacheKeyForObject`

```swift
var cacheKeyForObject: CacheKeyForObject?
```

> A function that returns a cache key for a particular result object. If it returns `nil`, a default cache key based on the field path will be used.

## Methods
### `clearCache(callbackQueue:completion:)`

```swift
func clearCache(callbackQueue: DispatchQueue, completion: ((Result<Void, Error>) -> Void)?)
```

> Clears the underlying cache.
> Be aware: In more complex setups, the same underlying cache can be used across multiple instances, so if you call this on one instance, it'll clear that cache across all instances which share that cache.
>
> - Parameters:
>   - callbackQueue: The queue to fall back on. Should default to the main queue.
>   - completion: [optional] A completion closure to execute when clearing has completed. Should default to nil.

#### Parameters

| Name | Description |
| ---- | ----------- |
| callbackQueue | The queue to fall back on. Should default to the main queue. |
| completion | [optional] A completion closure to execute when clearing has completed. Should default to nil. |

### `fetch(query:cachePolicy:context:queue:resultHandler:)`

```swift
func fetch<Query: GraphQLQuery>(query: Query,
```

> Fetches a query from the server or from the local cache, depending on the current contents of the cache and the specified cache policy.
>
> - Parameters:
>   - query: The query to fetch.
>   - cachePolicy: A cache policy that specifies when results should be fetched from the server and when data should be loaded from the local cache.
>   - context: [optional] A context to use for the cache to work with results. Should default to nil.
>   - queue: A dispatch queue on which the result handler will be called. Defaults to the main queue.
>   - resultHandler: [optional] A closure that is called when query results are available or when an error occurs.
> - Returns: An object that can be used to cancel an in progress fetch.

#### Parameters

| Name | Description |
| ---- | ----------- |
| query | The query to fetch. |
| cachePolicy | A cache policy that specifies when results should be fetched from the server and when data should be loaded from the local cache. |
| context | [optional] A context to use for the cache to work with results. Should default to nil. |
| queue | A dispatch queue on which the result handler will be called. Defaults to the main queue. |
| resultHandler | [optional] A closure that is called when query results are available or when an error occurs. |

### `watch(query:cachePolicy:queue:resultHandler:)`

```swift
func watch<Query: GraphQLQuery>(query: Query,
```

> Watches a query by first fetching an initial result from the server or from the local cache, depending on the current contents of the cache and the specified cache policy. After the initial fetch, the returned query watcher object will get notified whenever any of the data the query result depends on changes in the local cache, and calls the result handler again with the new result.
>
> - Parameters:
>   - query: The query to fetch.
>   - fetchHTTPMethod: The HTTP Method to be used.
>   - cachePolicy: A cache policy that specifies when results should be fetched from the server or from the local cache.
>   - queue: A dispatch queue on which the result handler will be called. Should default to the main queue.
>   - resultHandler: [optional] A closure that is called when query results are available or when an error occurs.
> - Returns: A query watcher object that can be used to control the watching behavior.

#### Parameters

| Name | Description |
| ---- | ----------- |
| query | The query to fetch. |
| fetchHTTPMethod | The HTTP Method to be used. |
| cachePolicy | A cache policy that specifies when results should be fetched from the server or from the local cache. |
| queue | A dispatch queue on which the result handler will be called. Should default to the main queue. |
| resultHandler | [optional] A closure that is called when query results are available or when an error occurs. |

### `perform(mutation:context:queue:resultHandler:)`

```swift
func perform<Mutation: GraphQLMutation>(mutation: Mutation,
```

> Performs a mutation by sending it to the server.
>
> - Parameters:
>   - mutation: The mutation to perform.
>   - context: [optional] A context to use for the cache to work with results. Should default to nil.
>   - queue: A dispatch queue on which the result handler will be called. Defaults to the main queue.
>   - resultHandler: An optional closure that is called when mutation results are available or when an error occurs.
> - Returns: An object that can be used to cancel an in progress mutation.

#### Parameters

| Name | Description |
| ---- | ----------- |
| mutation | The mutation to perform. |
| context | [optional] A context to use for the cache to work with results. Should default to nil. |
| queue | A dispatch queue on which the result handler will be called. Defaults to the main queue. |
| resultHandler | An optional closure that is called when mutation results are available or when an error occurs. |

### `upload(operation:context:files:queue:resultHandler:)`

```swift
func upload<Operation: GraphQLOperation>(operation: Operation,
```

> Uploads the given files with the given operation.
>
> - Parameters:
>   - operation: The operation to send
>   - context: [optional] A context to use for the cache to work with results. Should default to nil.
>   - files: An array of `GraphQLFile` objects to send.
>   - queue: A dispatch queue on which the result handler will be called. Should default to the main queue.
>   - completionHandler: The completion handler to execute when the request completes or errors
> - Returns: An object that can be used to cancel an in progress request.
> - Throws: If your `networkTransport` does not also conform to `UploadingNetworkTransport`.

#### Parameters

| Name | Description |
| ---- | ----------- |
| operation | The operation to send |
| context | [optional] A context to use for the cache to work with results. Should default to nil. |
| files | An array of `GraphQLFile` objects to send. |
| queue | A dispatch queue on which the result handler will be called. Should default to the main queue. |
| completionHandler | The completion handler to execute when the request completes or errors |

### `subscribe(subscription:queue:resultHandler:)`

```swift
func subscribe<Subscription: GraphQLSubscription>(subscription: Subscription,
```

> Subscribe to a subscription
>
> - Parameters:
>   - subscription: The subscription to subscribe to.
>   - fetchHTTPMethod: The HTTP Method to be used.
>   - queue: A dispatch queue on which the result handler will be called. Defaults to the main queue.
>   - resultHandler: An optional closure that is called when mutation results are available or when an error occurs.
> - Returns: An object that can be used to cancel an in progress subscription.

#### Parameters

| Name | Description |
| ---- | ----------- |
| subscription | The subscription to subscribe to. |
| fetchHTTPMethod | The HTTP Method to be used. |
| queue | A dispatch queue on which the result handler will be called. Defaults to the main queue. |
| resultHandler | An optional closure that is called when mutation results are available or when an error occurs. |