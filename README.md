# Telegraph
An event/message system for Unity

### This library requires [Odin Inspector](https://odininspector.com/)

Define event types (if not present in the library)

```csharp
public class FloatMessage : MessageBase<float> {}

[CreateAssetMenu(menuName = Telegraph.MENU_PATH + "Float", fileName = "Float Channel")]
public class FloatChannel : ChannelBase<FloatMessage, float> {}
```

Define your events in code

```cshapr
[Telegraph]
public static class Events
{
    [Telegram]
    public static Message StartGame => Telegraph.Get<Message>(nameof(StartGame));
    [Telegram]
    public static Message OnStartGame => Telegraph.Get<Message>(nameof(OnStartGame));
}

[Telegraph]
public static class PlayerEvents
{
    [Telegram]
    public static FloatMessage OnDamage => Telegraph.Get<FloatMessage>(nameof(OnDamage));
}
```

Register your methods to them

```cshapr
Events.StartGame.On += () => { Debug.Log("Game Started") }
```

Then you can fire them from code

```csharp
Events.StartGame.Raise()
PlayerEvents.OnDamage.Raise(5f)
```

You can also create scriptable object assets to reference the ones defined in code: `Create` -> `Red Owl` -> `Channel` -> `Void`

And then you can use normal methods to work with scriptable objects and call the methods on them (or even load them via addressables)

Lastly you can use `MessageListener` component to easily create a listener that will trigger the attached UnityEvent.

Everything is strongly typed!

Cheers

