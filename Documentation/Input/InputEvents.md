# Input Events

At the script level you consume input events by implementing one of the event handler interfaces shown in the table below.

> [!IMPORTANT]
> By default a script will receive events only while in focus by a pointer. To receive events while out of focus, in addition to implementing the desired handler interfaces, you have to do one of the following:
>
> - (Preferred) Register the script as a global listener via [`MixedRealityToolkit.InputSystem.RegisterHandler`](xref:Microsoft.MixedReality.Toolkit.IMixedRealityEventSystem) in `OnEnable` (`UnregisterHandler` explicitly in `OnDisable`). `RegisterHandler` needs to be called multiple times for listening to global input events on multiple interfaces. This method is preferred because `InputSystemGlobalHandlerListener` (see below) might be an unnecessary complication in most cases.
> - Derive the script from [`InputSystemGlobalHandlerListener`](xref:Microsoft.MixedReality.Toolkit.Input.InputSystemGlobalHandlerListener). This component is provided primarily to ease migration from `InputSystemGlobalListener`. It should also be used if having an `InputSystem` property on the component is beneficial (it is used in the rest of component's logic). It requires implementing its abstract methods `RegisterHandlers` and `UnregisterHandlers`. In these implementations [`MixedRealityToolkit.InputSystem.RegisterHandler`](xref:Microsoft.MixedReality.Toolkit.IMixedRealityEventSystem) should be used to list the interfaces the global events should be received for.

Handler | Events | Description
--- | --- | ---
[`IMixedRealitySourceStateHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealitySourceStateHandler) | Source Detected / Lost | Raised when an input source is detected/lost, like when an articulated hand is detected or lost track of.
[`IMixedRealitySourcePoseHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealitySourcePoseHandler) | Source Pose Changed | Raised on source pose changes. The source pose represents the general pose of the input source. Specific poses, like the grip or pointer pose in a six DOF controller, can be obtained via `IMixedRealityInputHandler<MixedRealityPose>`.
[`IMixedRealityInputHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityInputHandler) | Input Down / Up | Raised on changes to binary inputs like buttons.
[`IMixedRealityInputHandler<T>`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityInputHandler`1) | Input Changed | Raised on changes to inputs of the given type. **T** can take the following values: `float` (e.g. analog trigger), `Vector2` (e.g. gamepad thumbstick), `Vector3` (e.g. position-only tracked device), `Quaternion` (e.g. orientation-only tracked device) and [`MixedRealityPose`](xref:Microsoft.MixedReality.Toolkit.Utilities.MixedRealityPose) (e.g. fully tracked device).
[`IMixedRealitySpeechHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealitySpeechHandler) | Speech Keyword Recognized | Raised on recognition of one of the keywords configured in the *Speech Commands Profile*.
[`IMixedRealityDictationHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityDictationHandler) | Dictation Hypothesis / Result / Complete / Error | Raised by dictation systems to report the results of a dictation session.
[`IMixedRealityGestureHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityGestureHandler) | Gesture Started / Updated / Completed / Canceled | Raised on gesture detection.
[`IMixedRealityGestureHandler<T>`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityGestureHandler`1) | Gesture Updated / Completed | Raised on detection of gestures containing additional data of the given type. See [**Gesture Events**](Gestures.md#gesture-events) for details on possible values for **T**.
[`IMixedRealityHandJointHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityHandJointHandler) | Hand Joints Updated | Raised by articulated hand controllers when hand joints are updated.
[`IMixedRealityHandMeshHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityHandMeshHandler) | Hand Mesh Updated | Raised by articulated hand controllers when a hand mesh is updated.
[`IMixedRealityInputActionHandler`](xref:Microsoft.MixedReality.Toolkit.Input.IMixedRealityInputActionHandler) | Action Started / Ended | Raise to indicate action start and end for inputs mapped to actions.
