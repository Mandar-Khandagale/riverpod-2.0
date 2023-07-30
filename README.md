# <-- Riverpod-2.0 -->

## Defining a provider
Sync:--

Functional (Can’t perform side-effectsusing public methods)
```
@riverpod
String example(ExampleRef ref) {
  return 'foo';
}
```
Class-Based (Can perform side-effects using public methods)

```
@riverpod
class Example extends _$Example {
  @override
  String build() {
    return 'foo';
  }

  // Add methods to mutate the state
}
```

Async - Future:--

Functional (Can’t perform side-effectsusing public methods)
```
@riverpod
Future<String> example(ExampleRef ref) async {
  return Future.value('foo');
}
```
Class-Based (Can perform side-effects using publi  methods)

```
@riverpod
class Example extends _$Example {
  @override
  Future<String> build() async {
    return Future.value('foo');
  }

  // Add methods to mutate the state
}
```

Async - Stream:--

Functional (Can’t perform side-effectsusing public methods)
```
@riverpod
Stream<String> example(ExampleRef ref) async* {
  yield 'foo';
}
```
Class-Based (Can perform side-effects using publi  methods)

```
@riverpod
class Example extends _$Example {
  @override
  Stream<String> build() async* {
    yield 'foo';
  }

  // Add methods to mutate the state
}
```

## Enabling/disable autoDispose :--

```
// AutoDispose provider (keepAlive is false by default)
@riverpod
String example1(Example1Ref ref) => 'foo';

// Non autoDispose provider
@Riverpod(keepAlive: true)
String example2(Example2Ref ref) => 'foo';
```

## Passing parameters to a provider (family) :--

Functional
```
@riverpod
String example(
  ExampleRef ref,
  int param1, {
  String param2 = 'foo',
}) {
  return 'Hello $param1 & param2';
}
```

Class-Based

```
@riverpod
class Example extends _$Example {
  @override
  String build(
    int param1, {
    String param2 = 'foo',
  }) {
    return 'Hello $param1 & param2';
  }

  // Add methods to mutate the state
}
```

## Migrate from non-code-generation variant :--

### Provider :--

#### BEFORE
```
final exampleProvider = Provider.autoDispose<String>(
  (ref) {
    return 'foo';
  },
);
```

#### AFTER
```
@riverpod
String example(ExampleRef ref) {
  return 'foo';
}
```

### NotifierProvider :--

#### BEFORE
```
final exampleProvider = NotifierProvider.autoDispose<ExampleNotifier, String>(
  ExampleNotifier.new,
);

class ExampleNotifier extends AutoDisposeNotifier<String> {
  @override
  String build() {
    return 'foo';
  }

  // Add methods to mutate the state
}
```

#### AFTER
```
@riverpod
class Example extends _$Example {
  @override
  String build() {
    return 'foo';
  }

  // Add methods to mutate the state
}
```

### FutureProvider :--

#### BEFORE
```
final exampleProvider =
    FutureProvider.autoDispose<String>((ref) async {
  return Future.value('foo');
});
```

#### AFTER
```
@riverpod
Future<String> example(ExampleRef ref) async {
  return Future.value('foo');
}
```

### AsyncNotifierProvider :--

#### BEFORE
```
final exampleProvider =
    AsyncNotifierProvider.autoDispose<ExampleNotifier, String>(
  ExampleNotifier.new,
);

class ExampleNotifier extends AutoDisposeAsyncNotifier<String> {
  @override
  Future<String> build() async {
    return Future.value('foo');
  }

  // Add methods to mutate the state
}
```

#### AFTER
```
@riverpod
class Example extends _$Example {
  @override
  Future<String> build() async {
    return Future.value('foo');
  }

  // Add methods to mutate the state
}
```

### StreamNotifierProvider :--

#### BEFORE
```
final exampleProvider =
    StreamNotifierProvider.autoDispose<ExampleNotifier, String>(() {
  return ExampleNotifier();
});

class ExampleNotifier extends AutoDisposeStreamNotifier<String> {
  @override
  Stream<String> build() async* {
    yield 'foo';
  }

  // Add methods to mutate the state
}
```

#### AFTER
```
@riverpod
class Example extends _$Example {
  @override
  Stream<String> build() async* {
    yield 'foo';
  }

  // Add methods to mutate the state
}
```

