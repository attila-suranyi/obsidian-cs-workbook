# TDD practice

## Balázs's thoughts:

### What I like:
- GreedGame is built up on __dependency injection__
- All dependencies follow __Single Responsibility principle__, very Hardcore version
- GreedGameTest uses __mocking__ for it's dependencies which is super important, since only this way is possible to test the core game logic (nextTurn);
If we didn't mock the dependencies, if one is modified and breaks, it would break the GreedGameTest too, which is bad (since it's unmodified and works as intended)
- `@RepeatedTest` and `@ParameterizedTest` (with `@ValueSource` or `@MethodSource` ) are nice, and I liked the evolution of our tests
- Embedding these codes into Spring was like nothing, since TDD drove us towards a nicely built solution
- I had no doubt about the controller will work immediately and without bugs
- We have just the __right amount of production code__, I couldn't remove anything from it. This is the __YAGNI__ principle basically, and it's a result of TDD based codebase evolution

### What I didn't like:
- __No integration tests__. We really need a GreedGameIntegrationTest, where we don't mock the dependencies but use the implementations
- We should've made __interfaces__ on top of ScoreCalculator, since probably we would like to replace it later, the code is not clean at all
- We should've extracted some code to private methods for readability (only after the tests passed)
- We don't have integration tests with spring which could cause problems later on
- We didn't checked __corner cases__ for GreedGame, for example now it accepts 7+ dies as well, it's a problem (a full integration test would cover this)

