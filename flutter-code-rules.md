
This chapter's content comes from Flutter and third-party library official documentation, describing Dart code standards, Dart 3 new syntax, Flutter application architecture, ChangeNotifier & Provider state management, Mocktail testing and other best practices, for reference only and can be flexibly applied.

### Effective Dart Rules

#### Naming Conventions

1. Use terms consistently throughout your code.
2. Follow existing mnemonic conventions when naming type parameters (e.g., `E` for element, `K`/`V` for key/value, `T`/`S`/`U` for generic types).
3. Name types using `UpperCamelCase` (classes, enums, typedefs, type parameters).
4. Name extensions using `UpperCamelCase`.
5. Name packages, directories, and source files using `lowercase_with_underscores`.
6. Name import prefixes using `lowercase_with_underscores`.
7. Name other identifiers using `lowerCamelCase` (variables, parameters, named parameters).
8. Capitalize acronyms and abbreviations longer than two letters like words.
9. Avoid abbreviations unless the abbreviation is more common than the unabbreviated term.
10. Prefer putting the most descriptive noun last in names.
11. Consider making code read like a sentence when designing APIs.
12. Prefer a noun phrase for non-boolean properties or variables.
13. Prefer a non-imperative verb phrase for boolean properties or variables.
14. Prefer the positive form for boolean property and variable names.
15. Consider omitting the verb for named boolean parameters.
16. Use camelCase for variable and function names.
17. Use PascalCase for class names.
18. Use snake_case for file names.

#### Types and Functions

1. Use class modifiers to control if your class can be extended or used as an interface.
2. Type annotate variables without initializers.
3. Type annotate fields and top-level variables if the type isn't obvious.
4. Annotate return types on function declarations.
5. Annotate parameter types on function declarations.
6. Write type arguments on generic invocations that aren't inferred.
7. Annotate with `dynamic` instead of letting inference fail.
8. Use `Future<void>` as the return type of asynchronous members that do not produce values.
9. Use getters for operations that conceptually access properties.
10. Use setters for operations that conceptually change properties.
11. Use a function declaration to bind a function to a name.
12. Use inclusive start and exclusive end parameters to accept a range.

#### Style

1. Format your code using `dart format`.
2. Use curly braces for all flow control statements.
3. Prefer `final` over `var` when variable values won't change.
4. Use `const` for compile-time constants.

#### Imports & Files

1. Don't import libraries inside the `src` directory of another package.
2. Don't allow import paths to reach into or out of `lib`.
3. Prefer relative import paths within a package.
4. Don't use `/lib/` or `../` in import paths.
5. Consider writing a library-level doc comment for library files.

#### Structure

1. Keep files focused on a single responsibility.
2. Limit file length to maintain readability.
3. Group related functionality together.
4. Prefer making fields and top-level variables `final`.
5. Consider making your constructor `const` if the class supports it.
6. Prefer making declarations private.

#### Usage

1. Use strings in `part of` directives.
2. Use adjacent strings to concatenate string literals.
3. Use collection literals when possible.
4. Use `whereType()` to filter a collection by type.
5. Test for `Future<T>` when disambiguating a `FutureOr<T>` whose type argument could be `Object`.
6. Follow a consistent rule for `var` and `final` on local variables.
7. Initialize fields at their declaration when possible.
8. Use initializing formals when possible.
9. Use `;` instead of `{}` for empty constructor bodies.
10. Use `rethrow` to rethrow a caught exception.
11. Override `hashCode` if you override `==`.
12. Make your `==` operator obey the mathematical rules of equality.

#### Documentation

1. Format comments like sentences.
2. Use `///` doc comments to document members and types; don't use block comments for documentation.
3. Prefer writing doc comments for public APIs.
4. Consider writing doc comments for private APIs.
5. Consider including explanations of terminology, links, and references in library-level docs.
6. Start doc comments with a single-sentence summary.
7. Separate the first sentence of a doc comment into its own paragraph.
8. Use square brackets in doc comments to refer to in-scope identifiers.
9. Use prose to explain parameters, return values, and exceptions.
10. Put doc comments before metadata annotations.
11. Document why code exists or how it should be used, not just what it does.

#### Testing

1. Write unit tests for business logic.
2. Write widget tests for UI components.
3. Aim for good test coverage.

#### Widgets

1. Extract reusable widgets into separate components.
2. Use `StatelessWidget` when possible.
3. Keep build methods simple and focused.

#### State Management

1. Choose appropriate state management based on complexity.
2. Avoid unnecessary `StatefulWidget`s.
3. Keep state as local as possible.

#### Performance

1. Use `const` constructors when possible.
2. Avoid expensive operations in build methods.
3. Implement pagination for large lists.

### Dart 3 Updates

#### Branches

1. Use `if` statements for conditional branching. The condition must evaluate to a boolean.
2. `if` statements support optional `else` and `else if` clauses for multiple branches.
3. Use `if-case` statements to match and destructure a value against a single pattern. Example: `if (pair case [int x, int y]) { ... }`
4. If the pattern in an `if-case` matches, variables defined in the pattern are in scope for that branch.
5. If the pattern does not match in an `if-case`, control flows to the `else` branch if present.
6. Use `switch` statements to match a value against multiple patterns (cases). Each `case` can use any kind of pattern.
7. When a value matches a `case` pattern in a `switch` statement, the case body executes and control jumps to the end of the switch. `break` is not required.
8. You can end a non-empty `case` clause with `continue`, `throw`, or `return`.
9. Use `default` or `_` in a `switch` statement to handle unmatched values.
10. Empty `case` clauses fall through to the next case. Use `break` to prevent fallthrough.
11. Use `continue` with a label for non-sequential fallthrough between cases.
12. Use logical-or patterns (e.g., `case a || b`) to share a body or guard between cases.
13. Use `switch` expressions to produce a value based on matching cases. Syntax differs from statements: omit `case`, use `=>` for bodies, and separate cases with commas.
14. In `switch` expressions, the default case must use `_` (not `default`).
15. Dart checks for exhaustiveness in `switch` statements and expressions, reporting a compile-time error if not all possible values are handled.
16. To ensure exhaustiveness, use a default (`default` or `_`) case, or switch over enums or sealed types.
17. Use the `sealed` modifier on a class to enable exhaustiveness checking when switching over its subtypes.
18. Add a guard clause to a `case` using `when` to further constrain when a case matches. Example: `case pattern when condition:`
19. Guard clauses can be used in `if-case`, `switch` statements, and `switch` expressions. The guard is evaluated after pattern matching.
20. If a guard clause evaluates to false, execution proceeds to the next case (does not exit the switch).

#### Patterns

1. Patterns are a syntactic category that represent the shape of values for matching and destructuring.
2. Pattern matching checks if a value has a certain shape, constant, equality, or type.
3. Pattern destructuring allows extracting parts of a matched value and binding them to variables.
4. Patterns can be nested, using subpatterns (outer/inner patterns) for recursive matching and destructuring.
5. Use wildcard patterns (`_`) to ignore parts of a matched value; use rest elements in list patterns to ignore remaining elements.
6. Patterns can be used in:
   - Local variable declarations and assignments
   - For and for-in loops
   - If-case and switch-case statements
   - Control flow in collection literals
7. Pattern variable declarations start with `var` or `final` and bind new variables from the matched value. Example: `var (a, [b, c]) = ('str', [1, 2]);`
8. Pattern variable assignments destructure a value and assign to existing variables. Example: `(b, a) = (a, b); // swap values`
9. Every case clause in `switch` and `if-case` contains a pattern. Any kind of pattern can be used in a case.
10. Case patterns are refutable; if the pattern doesn't match, execution continues to the next case.
11. Destructured values in a case become local variables scoped to the case body.
12. Use logical-or patterns (e.g., `case a || b`) to match multiple alternatives in a single case.
13. Use logical-or patterns with guards (`when`) to share a body or guard between cases.
14. Guard clauses (`when`) evaluate a condition after matching; if false, execution proceeds to the next case.
15. Patterns can be used in for and for-in loops to destructure collection elements (e.g., destructuring `MapEntry` in map iteration).
16. Object patterns match named object types and destructure their data using getters. Example: `var Foo(:one, :two) = myFoo;`
17. Use patterns to destructure records, including positional and named fields, directly into local variables.
18. Patterns enable algebraic data type style code: use sealed classes and switch on subtypes for exhaustive matching.
19. Patterns simplify validation and destructuring of complex data structures, such as JSON, in a declarative way. Example: `if (data case {'user': [String name, int age]}) { ... }`
20. Patterns provide a concise alternative to verbose type-checking and destructuring code.

#### Pattern Types

1. Pattern precedence determines evaluation order; use parentheses to group lower-precedence patterns.
2. Logical-or patterns (`pattern1 || pattern2`) match if any branch matches, evaluated left-to-right. All branches must bind the same set of variables.
3. Logical-and patterns (`pattern1 && pattern2`) match if both subpatterns match. Bound variable names must not overlap between subpatterns.
4. Relational patterns (`==`, `!=`, `<`, `>`, `<=`, `>=`) match if the value compares as specified to a constant. Useful for numeric ranges and can be combined with logical-and.
5. Cast patterns (`subpattern as Type`) assert and cast a value to a type before passing it to a subpattern. Throws if the value is not of the type.
6. Null-check patterns (`subpattern?`) match if the value is not null, then match the inner pattern. Binds the non-nullable type. Use constant pattern `null` to match null.
7. Null-assert patterns (`subpattern!`) match if the value is not null, else throw. Use in variable declarations to eliminate nulls. Use constant pattern `null` to match null.
8. Constant patterns match if the value is equal to a constant (number, string, bool, named constant, const constructor, const collection, etc.). Use parentheses and `const` for complex expressions.
9. Variable patterns (`var name`, `final Type name`) bind new variables to matched/destructured values. Typed variable patterns only match if the value has the declared type.
10. Identifier patterns (`foo`, `_`) act as variable or constant patterns depending on context. `_` always acts as a wildcard and matches/discards any value.
11. Parenthesized patterns (`(subpattern)`) control pattern precedence and grouping, similar to expressions.
12. List patterns (`[subpattern1, subpattern2]`) match lists and destructure elements by position. The pattern length must match the list unless a rest element is used.
13. Rest elements (`...`, `...rest`) in list patterns match arbitrary-length lists or collect unmatched elements into a new list.
14. Map patterns (`{"key": subpattern}`) match maps and destructure by key. Only specified keys are matched; missing keys throw a `StateError`.
15. Record patterns (`(subpattern1, subpattern2)`, `(x: subpattern1, y: subpattern2)`) match records by shape and destructure positional/named fields. Field names can be omitted if inferred from variable or identifier patterns.
16. Object patterns (`ClassName(field1: subpattern1, field2: subpattern2)`) match objects by type and destructure using getters. Extra fields in the object are ignored.
17. Wildcard patterns (`_`, `Type _`) match any value without binding. Useful for ignoring values or type-checking without binding.
18. All pattern types can be nested and combined for expressive and precise matching and destructuring.

#### Records

1. Records are anonymous, immutable, aggregate types that bundle multiple objects into a single value.
2. Records are fixed-sized, heterogeneous, and strongly typed. Each field can have a different type.
3. Records are real values: store them in variables, nest them, pass to/from functions, and use in lists, maps, and sets.
4. Record expressions use parentheses with comma-delimited positional and/or named fields, e.g. `('first', a: 2, b: true, 'last')`.
5. Record type annotations use parentheses with comma-delimited types. Named fields use curly braces: `({int a, bool b})`.
6. The names of named fields are part of the record's type (shape). Records with different named field names have different types.
7. Positional field names in type annotations are for documentation only and do not affect the record's type.
8. Record fields are accessed via built-in getters: positional fields as `$1`, `$2`, etc., and named fields by their name (e.g., `.a`).
9. Records are immutable: fields do not have setters.
10. Records are structurally typed: the set, types, and names of fields define the record's type (shape).
11. Two records are equal if they have the same shape and all corresponding field values are equal. Named field order does not affect equality.
12. Records automatically define `hashCode` and `==` based on structure and field values.
13. Use records for functions that return multiple values; destructure with pattern matching: `var (name, age) = userInfo(json);`
14. Destructure named fields with the colon syntax: `final (:name, :age) = userInfo(json);`
15. Using records for multiple returns is more concise and type-safe than using classes, lists, or maps.
16. Use lists of records for simple data tuples with the same shape.
17. Use type aliases (`typedef`) for record types to improve readability and maintainability.
18. Changing a record type alias does not guarantee all code using it is still type-safe; only classes provide full abstraction/encapsulation.
19. Extension types can wrap records but do not provide full abstraction or protection.
20. Records are best for simple, immutable data aggregation; use classes for abstraction, encapsulation, and behavior.

### Flutter App Architecture

1. Separate your features into a UI Layer (presentation), a Data Layer (business data and logic), and, for complex apps, consider adding a Domain (Logic) Layer between UI and Data layers to encapsulate business logic and use-cases.
2. You can organize code by feature: The classes needed for each feature are grouped together. For example, you might have an auth directory, which would contain files like auth_viewmodel.dart (or, depending on your state management approach: auth_controller.dart, auth_provider.dart, auth_bloc.dart), login_usecase.dart, logout_usecase.dart, login_screen.dart, logout_button.dart, etc. Alternatively, you can organize by type or use a hybrid approach.
3. Only allow communication between adjacent layers; the UI layer should not access the data layer directly, and vice versa.
4. Introduce a Logic (Domain) Layer only for complex business logic that does not fit cleanly in the UI or Data layers.
5. Clearly define the responsibilities, boundaries, and interfaces of each layer and component (Views, View Models, Repositories, Services).
6. Further divide each layer into components with specific responsibilities and well-defined interfaces.
7. In the UI Layer, use Views to describe how to present data to the user; keep logic minimal and only UI-related.
8. Pass events from Views to View Models in response to user interactions.
9. In View Models, contain logic to convert app data into UI state and maintain the current state needed by the view.
10. Expose callbacks (commands) from View Models to Views and retrieve/transform data from repositories.
11. In the Data Layer, use Repositories as the single source of truth (SSOT) for model data and to handle business logic such as caching, error handling, and refreshing data.
12. Only the SSOT class (usually the repository) should be able to mutate its data; all other classes should read from it.
13. Repositories should transform raw data from services into domain models and output data consumed by View Models.
14. Use Services to wrap API endpoints and expose asynchronous response objects; services should isolate data-loading and hold no state.
15. Use dependency injection to provide components with their dependencies, enabling testability and flexibility.

#### Data Flow and State

1. Follow unidirectional data flow: state flows from the data layer through the logic layer to the UI layer, and events from user interaction flow in the opposite direction.
2. Data changes should always happen in the SSOT (data layer), not in the UI or logic layers.
3. The UI should always reflect the current (immutable) state; trigger UI rebuilds only in response to state changes.
4. Views should contain as little logic as possible and be driven by state from View Models.

#### Use Cases / Interactors

1. Introduce use cases/interactors in the domain layer only when logic is complex, reused, or merges data from multiple repositories.
2. Use cases depend on repositories and may be used by multiple view models.
3. Add use cases only when needed; refactor to use use-cases exclusively if logic is repeatedly shared across view models.

#### Extensibility and Testability

1. All architectural components should have well-defined inputs and outputs (interfaces).
2. Favor dependency injection to allow swapping implementations without changing consumers.
3. Test view models by mocking repositories; test UI logic independently of widgets.
4. Design components to be easily replaceable and independently testable.

#### Best Practices

1. Strongly recommend following separation of concerns and layered architecture.
2. Strongly recommend using dependency injection for testability and flexibility.
3. Recommend using MVVM as the default pattern, but adapt as needed for your app's complexity.
4. Use key-value storage for simple data (e.g., configuration, preferences) and SQL storage for complex relationships.
5. Use optimistic updates to improve perceived responsiveness by updating the UI before operations complete.
6. Support offline-first strategies by combining local and remote data sources in repositories and enabling synchronization as appropriate.
7. Keep views focused on presentation and extract reusable widgets into separate components.
8. Use `StatelessWidget` when possible and avoid unnecessary `StatefulWidget`s.
9. Keep build methods simple and focused on rendering.
10. Choose state management approaches appropriate to the complexity of your app.
11. Keep state as local as possible to minimize rebuilds and complexity.
12. Use `const` constructors when possible to improve performance.
13. Avoid expensive operations in build methods and implement pagination for large lists.
14. Keep files focused on a single responsibility and limit file length for readability.
15. Group related functionality together and use `final` for fields and top-level variables when possible.
16. Prefer making declarations private and consider making constructors `const` if the class supports it.
17. Follow Dart naming conventions and format code using `dart format`.
18. Use curly braces for all flow control statements to ensure clarity and prevent bugs.

### Flutter ChangeNotifier State Management Rules

1. Place shared state above the widgets that use it in the widget tree to enable proper rebuilds and avoid imperative UI updates.
2. Avoid directly mutating widgets or calling methods on them to change state; instead, rebuild widgets with new data.
3. Use a model class that extends `ChangeNotifier` to manage and notify listeners of state changes.

```dart
class CartModel extends ChangeNotifier {
  final List<Item> _items = [];
  UnmodifiableListView<Item> get items => UnmodifiableListView(_items);

  void add(Item item) {
    _items.add(item);
    notifyListeners();
  }
}
```

4. Keep internal state private within the model and expose unmodifiable views to the UI.
5. Call `notifyListeners()` in your model whenever the state changes to trigger UI rebuilds.
6. Use `ChangeNotifierProvider` to provide your model to the widget subtree that needs access to it.

```dart
ChangeNotifierProvider(
  create: (context) => CartModel(),
  child: MyApp(),
)
```

7. Wrap widgets that depend on the model’s state in a `Consumer<T>` widget to rebuild only when relevant data changes.

```dart
return Consumer<CartModel>(
  builder: (context, cart, child) => Stack(
    children: [
      if (child != null) child,
      Text('Total price: \${cart.totalPrice}'),
    ],
  ),
  child: const SomeExpensiveWidget(),
);
```

8. Always specify the generic type `<T>` for `Consumer<T>` and `Provider.of<T>` to ensure type safety and correct behavior.
9. Use the `child` parameter of `Consumer` to optimize performance by preventing unnecessary rebuilds of widgets that do not depend on the model.
10. Place `Consumer` widgets as deep in the widget tree as possible to minimize the scope of rebuilds.

```dart
return HumongousWidget(
  child: AnotherMonstrousWidget(
    child: Consumer<CartModel>(
      builder: (context, cart, child) {
        return Text('Total price: \${cart.totalPrice}');
      },
    ),
  ),
);
```

11. Do not wrap large widget subtrees in a `Consumer` if only a small part depends on the model; instead, wrap only the part that needs to rebuild.
12. Use `Provider.of<T>(context, listen: false)` when you need to access the model for actions (such as calling methods) but do not want the widget to rebuild on state changes.

```dart
Provider.of<CartModel>(context, listen: false).removeAll();
```

13. `ChangeNotifierProvider` automatically disposes of the model when it is no longer needed.
14. Use `MultiProvider` when you need to provide multiple models to the widget tree.
15. Write unit tests for your `ChangeNotifier` models to verify state changes and notifications.
16. Avoid rebuilding widgets unnecessarily; optimize rebuilds by structuring your widget tree and provider usage carefully.

### Common Flutter Errors

1. If you get a "RenderFlex overflowed" error, check if a `Row` or `Column` contains unconstrained widgets. Fix by wrapping children in `Flexible`, `Expanded`, or by setting constraints.
2. If you get "Vertical viewport was given unbounded height", ensure `ListView` or similar scrollable widgets inside a `Column` have a bounded height (e.g., wrap with `Expanded` or `SizedBox`).
3. If you get "An InputDecorator...cannot have an unbounded width", constrain the width of widgets like `TextField` using `Expanded`, `SizedBox`, or by placing them in a parent with width constraints.
4. If you get a "setState called during build" error, do not call `setState` or `showDialog` directly inside the build method. Trigger dialogs or state changes in response to user actions or after the build completes (e.g., using `addPostFrameCallback`).
5. If you get "The ScrollController is attached to multiple scroll views", make sure each `ScrollController` is only attached to a single scrollable widget at a time.
6. If you get a "RenderBox was not laid out" error, check for missing or unbounded constraints in your widget tree. This is often caused by using widgets like `ListView` or `Column` without proper size constraints.
7. Use the Flutter Inspector and review widget constraints to debug layout issues. Refer to the official documentation on constraints if needed.

### Provider Rules

1. Use `Provider`, `ChangeNotifierProvider`, `FutureProvider`, and `StreamProvider` to expose values and manage state in the widget tree.
2. Always specify the generic type when using `Provider`, `Consumer`, `context.watch`, `context.read`, or `context.select` for type safety.

```dart
final value = context.watch<int>();
```

3. Use `ChangeNotifierProvider` to automatically dispose of the model when it is no longer needed.

```dart
ChangeNotifierProvider(
  create: (_) => MyNotifier(),
  child: MyApp(),
)
```

4. For objects that depend on other providers or values that may change, use `ProxyProvider` or `ChangeNotifierProxyProvider` instead of creating the object from variables that can change over time.

```dart
ProxyProvider0(
  update: (_, __) => MyModel(count),
  child: ...
)
```

5. Use `MultiProvider` to group multiple providers and avoid deeply nested provider trees.

```dart
MultiProvider(
  providers: [
    Provider<Something>(create: (_) => Something()),
    Provider<SomethingElse>(create: (_) => SomethingElse()),
  ],
  child: someWidget,
)
```

6. Use `context.watch<T>()` to listen to changes and rebuild the widget when `T` changes.
7. Use `context.read<T>()` to access a provider without listening for changes (e.g., in callbacks).
8. Use `context.select<T, R>(R selector(T value))` to listen to only a small part of `T` and optimize rebuilds.

```dart
final selected = context.select<MyModel, int>((model) => model.count);
```

9. Use `Consumer<T>` or `Selector<T, R>` widgets for fine-grained rebuilds when you cannot access a descendant `BuildContext`.

```dart
Consumer<MyModel>(
  builder: (context, value, child) => Text('$value'),
)
```

10. To migrate from `ValueListenableProvider`, use `Provider` with `ValueListenableBuilder`.

```dart
ValueListenableBuilder<int>(
  valueListenable: myValueListenable,
  builder: (context, value, _) {
    return Provider<int>.value(
      value: value,
      child: MyApp(),
    );
  }
)
```

11. Do not create your provider’s object from variables that can change over time; otherwise, the object will not update when the value changes.
12. For debugging, implement `toString` or use `DiagnosticableTreeMixin` to improve how your objects appear in Flutter DevTools.

```dart
class MyClass with DiagnosticableTreeMixin {
  // ...
  @override
  String toString() => '$runtimeType(a: $a, b: $b)';
}
```

13. Do not attempt to obtain providers inside `initState` or `constructor`; use them in `build`, callbacks, or lifecycle methods where the widget is fully mounted.
14. You can use any object as state, not just `ChangeNotifier`; use `Provider.value()` with a `StatefulWidget` if needed.
15. If you have a very large number of providers (e.g., 150+), consider mounting them over time (e.g., during splash screen animation) or avoid `MultiProvider` to prevent StackOverflowError.

### Mocktail Rules

1. Use a `Fake` when you need a lightweight, custom implementation of a class for testing, especially if you only need to override a subset of methods or provide specific behavior.
2. Use a `Mock` when you need to verify interactions (method calls, arguments, call counts) or need to stub method responses dynamically during tests.
3. Use `registerFallbackValue` to register a default value for a type that is used as an argument in a mock method, especially when the type is not nullable and is required for argument matching (e.g., `registerFallbackValue(MyCustomEvent())`).
4. Extend `Mock` to create a mock class for the class or interface you want to mock.
5. Use `when(() => mock.method()).thenReturn(value)` to stub method calls, and `thenThrow(error)` to stub errors.
6. Use `when(() => mock.method()).thenAnswer((invocation) => value)` for dynamic responses.
7. Use `verify(() => mock.method())` to check if a method was called; use `verifyNever(() => mock.method())` to check it was never called.
8. Use `verify(() => mock.method()).called(n)` to check the exact number of invocations.
9. Use argument matchers like `any()`, `captureAny()`, and `captureThat()` for flexible verification and stubbing.
10. Always register fallback values for custom types used with argument matchers before using them in stubs or verifications.
11. Prefer using real objects over mocks when possible; if not, use a tested fake implementation (`extends Fake`) over a mock.
12. Never add implementation or `@override` methods to a class extending `Mock`.
13. Only use mocks if your test asserts on interactions (calls to `verify`); otherwise, prefer real or fake objects.
14. Always stub async methods (returning `Future` or `Future<void>`) with `thenAnswer((_) async {})` or `thenReturn(Future.value(...))`.
15. Always include all named parameters in both `when` and `verify` calls, even if you only care about one. Use `any(named: 'paramName')` for those you don't care about.
16. If a method has default values for named parameters, Mocktail still expects all of them to be matched in both stubs and verifies.
17. Use `any()` for positional parameters in `when`/`verify` if you don't care about the exact instance.
18. Register fallback values for any custom types that are used with argument matchers before using them in your tests.
19. Stub every method you expect to be called, even if it's not the focus of your test, to prevent runtime errors.
20. When matching string outputs, make sure you understand what `.toString()` returns for the type you are using.
