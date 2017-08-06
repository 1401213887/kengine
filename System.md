# System

A system holds game logic.

`Systems` are also [Modules](putils/mediator/README.md), the `EntityManager` being their `Mediator`. This lets `Systems` easily communicate through `DataPackets`.

### Members

##### Definition

```
template<typename CRTP, typename ...DataPackets>
class System;
```

A `System` is defined by its sub-type (see `CRTP`) and the list of `DataPackets` types it would like to receive.

##### execute

```
virtual void execute() = 0;
```
Runs the system's game logic. Called each frame.

##### registerGameObject

```
virtual void registerGameObject(GameObject &go) {}
```
Automatically called for each new `GameObject`.

##### removeGameObject

```
virtual void removeGameObject(GameObject &go) {}
```
Automatically called for each `GameObject` that is removed.

##### getFrameRate

```
virtual std::size_t getFrameRate() const noexcept { return 60; }
```
Returns how many times `execute` should be called each second.

Should return 0 if the framerate shouldn't be limited.

##### time

Each `System` has a `time` member that exposes the following functions:

```
putils::Timer::t_duration getDeltaTime() const;
```
Returns the time since the last call to `execute`.

```
putils::Timee::t_duration getFixedDeltaTime() const;
```
Returns the expected time between two calls to execute, as determined by `getFrameRate`.

The `time` member structure is automatically managed by the `SystemManager`.
