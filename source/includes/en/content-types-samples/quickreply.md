## Quick Replies

```csharp
using System;
using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Lime.Messaging.Contents;
using Lime.Protocol;
using Take.Blip.Client;

public class PlainTextMessageReceiver : IMessageReceiver
{
private readonly ISender _sender;
private readonly Settings _settings;

public PlainTextMessageReceiver(ISender sender, Settings settings)
{
    _sender = sender;
    _settings = settings;
}

public async Task ReceiveAsync(Message message, CancellationToken cancellationToken)
{
    jsonDocuments = new JsonDocument();
    jsonDocuments.Add("Key1", "value1");
    jsonDocuments.Add("Key2", "2");

    Document document = new Select
    {
        Scope = SelectScope.Immediate,// (create a quickreply instead menu)
        Text = "Choice an option:",
        Options = new SelectOption[]
        {
            new SelectOption
            {
                Order = 1,
                Text = "First option!",
                Value = new PlainText { Text = "1" }
            },
            new SelectOption
            {
                Order = 2,
                Text = "Second option",
                Value = new PlainText { Text = "2" }
            },
            new SelectOption
            {
                Order = 3,
                Text = "Third option",
                Value = jsonDocuments
            }
        }
    };

    await _sender.SendMessageAsync(document, message.From, cancellationToken);
}
}
```

Quick replies provide a way to present a set of up to 11 buttons in-conversation that contain a title and optional image, and appear prominently above the composer. You can also use quick replies to request a person's location.

You can send quick replies by using [Select](/#select).


| Messenger                         | BLiPChat                                   |
|-----------------------------------|--------------------------------------------|
| ![imagem](images/quickreply_mssgnr.png) | ![imagem](quickReplyBlipChat.png)    |