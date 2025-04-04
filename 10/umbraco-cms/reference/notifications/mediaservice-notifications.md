---
versionFrom: 9.0.0
versionTo: 10.0.0
---

# MediaService Notifications

The MediaService class implements IMediaService. It provides access to operations involving IMedia.

## Usage

Example usage of the MediaService notifications:

```C#
using Microsoft.Extensions.Logging;
using Umbraco.Cms.Core.Events;
using Umbraco.Cms.Core.Notifications;

namespace MySite
{
    public class MediaNotificationHandler : INotificationHandler<MediaSavedNotification>
    {
        private readonly ILogger<MediaNotificationHandler> _logger;

        public MediaNotificationHandler(ILogger<MediaNotificationHandler> logger)
        {
            _logger = logger;
        }
        
        public void Handle(MediaSavedNotification notification)
        {
            foreach (var mediaItem in notification.SavedEntities)
            {
                if (mediaItem.ContentType.Alias.Equals("Image"))
                {
                    // Do something with the image, maybe send to Azure for AI analysis of image contents or something.
                    _logger.LogDebug($"Sending {mediaItem.Name} to analysis");
                    SendToAzure(mediaItem);
                }
            }
        }
    }
}
```

## Events

<table>
  <tr>
    <th>Notification</th>
    <th>Members</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>MediaSavingNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltIMedia&gt SavedEntities</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
        <li>bool Cancel</li>
      </ul>
    </td>
    <td>
    Published when MediaService.Save is called in the API.<br/>
    NOTE: It can be skipped completely if the parameter "raiseEvents" is set to false during the Save method call (true by default).<br/>
    SavedEntities: Gets the collection of IMedia objects being saved.
    </td>
  </tr>

  <tr>
    <td>MediaSavedNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltIMedia&gt SavedEntities</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
      </ul>
    </td>
    <td>
    Published when MediaService.Save is called in the API and after the data has been persisted.<br/>
    NOTE: It can be skipped completely if the parameter "raiseEvents" is set to false during the Save method call (true by default).<br/>
    SavedEntities: Gets the saved collection of IMedia objects.
    </td>
  </tr>

  <tr>
    <td>MediaMovingNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltMoveEventInfo&ltIMedia&gt&gt MoveInfoCollection</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
        <li>bool Cancel</li>
      </ul>
    </td>
    <td>
    Published when MediaService.Move is called in the API.<br/>
    NOTE: If the target parent is the Recycle bin, this notification is never published. Try the MediaMovingToRecycleBinNotification instead.<br/>
    MoveInfoCollection will for each moving entity provide:
      <ol>
        <li>Entity: Gets the IMedia object being moved</li>
        <li>OriginalPath: The original path the entity is moved from</li>
        <li>NewParentId: Gets the Id of the parent the entity will have after it has been moved</li>
      </ol>
    </td>
  </tr>

  <tr>
    <td>MediaMovedNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltMoveEventInfo&ltIMedia&gt&gt MoveInfoCollection</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
      </ul>
    </td>
    <td>
    Published when MediaService.Move is called in the API.
    The event is fired after the media object has been moved.<br/>
    NOTE: If the target parent is the Recycle bin, this notification is never published. Try the MediaMovedToRecycleBinNotification instead.<br/>
    MoveInfoCollection will for each moving entity provide:
      <ol>
        <li>Entity: Gets the IMedia object being moved</li>
        <li>OriginalPath: The original path the entity is moved from</li>
        <li>NewParentId: Gets the Id of the parent the entity will have after it has been moved</li>
      </ol>
    </td>
  </tr>

  <tr>
    <td>MediaMovingToRecycleBinNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltMoveEventInfo&ltIMedia&gt&gt MoveInfoCollection</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
        <li>bool Cancel</li>
      </ul>
    </td>
    <td>
    Published when MediaService.MoveToRecycleBin is called in the API.<br/>
    MoveInfoCollection will for each moving entity provide:
      <ol>
        <li>Entity: Gets the IMedia object being moved</li>
        <li>OriginalPath: The original path the entity is moved from</li>
        <li>NewParentId: Gets the Id of the RecycleBin</li>
      </ol>
    </td>
  </tr>

  <tr>
    <td>MediaMovedToRecycleBinNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltMoveEventInfo&ltIMedia&gt&gt MoveInfoCollection</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
      </ul>
    </td>
    <td>
    Published when MediaService.MoveToRecycleBin is called in the API, after the media object has been moved to the RecycleBin.<br/>
    MoveInfoCollection will for each moving entity provide:
      <ol>
        <li>Entity: Gets the IMedia object being moved</li>
        <li>OriginalPath: The original path the entity is moved from</li>
        <li>NewParentId: Gets the Id of the RecycleBin</li>
      </ol>
    </td>
  </tr>

  <tr>
    <td>MediaDeletingNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltIMedia&gt DeletedEntities</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
        <li>bool Cancel</li>
      </ul>
    </td>
    <td>
    Published when MediaService.DeleteMediaOfType, MediaService.Delete, MediaService.EmptyRecycleBin are called in the API.<br/>
    DeletedEntities: Gets the collection of IMedia objects being deleted.
    </td>
  </tr>

  <tr>
    <td>MediaDeletedNotification</td>
    <td>
      <ul>
        <li>IEnumerable&ltIMedia&gt DeletedEntities</li>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
      </ul>
    </td>
    <td>
    Published when MediaService.Delete, MediaService.EmptyRecycleBin are called in the API, after the media has been deleted.<br/>
    DeletedEntities: Gets the collection of deleted IMedia objects.
    </td>
  </tr>

  <tr>
    <td>MediaDeletingVersionsNotification</td>
    <td>
      <ul>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
        <li>bool Cancel</li>
        <li>int Id</li>
        <li>int SpecificVersion</li>
        <li>DateTime DateToRetain</li>
        <li>bool DeletePriorVersions</li>
      </ul>
    </td>
    <td>
    Published when MediaService.DeleteVersion, MediaService.DeleteVersions are called in the API.<br/>
      <ol>
        <li>Id: Gets the id of the IMedia object being deleted.</li>
        <li>DateToRetain: Gets the latest version date.</li>
        <li>SpecificVersion: Gets the id of the IMedia object version being deleted.</li>
        <li>DeletePriorVersions: False by default</li>
      </ol>
    </td>
  </tr>

  <tr>
    <td>MediaDeletedVersionsNotification</td>
    <td>
      <ul>
        <li>EventMessages Messages</li>
        <li>IDictionary&ltstring,object&gt State</li>
        <li>int Id</li>
        <li>int SpecificVersion</li>
        <li>DateTime DateToRetain</li>
        <li>bool DeletePriorVersions</li>
      </ul>
    </td>
    <td>
    Published when MediaService.DeleteVersion, MediaService.DeleteVersions are called in the API, after the media version has been deleted<br/>
      <ol>
        <li>Id: Gets the id of the deleted IMedia object.</li>
        <li>DateToRetain: Gets the latest version date.</li>
        <li>SpecificVersion: Gets the id of the deleted IMedia object version.</li>
        <li>DeletePriorVersions: False by default</li>
      </ol>
    </td>
  </tr>
</table>

### What happened to Creating and Created events?

Both the MediaService.Creating and MediaService.Created events have been obsoleted. Because of this, these were not moved over to notifications, and no longer exist. Why? Because these events were not guaranteed to trigger and therefore should not have been used. This is because these events *only* triggered when the MediaService.CreateMedia method was used which is an entirely optional way to create media entities. It is also possible to construct a new media item - which is generally the preferred and consistent way - and therefore the Creating/Created events would not execute when constructing media that way.

Furthermore, there was no reason to listen for the Creating/Created events because they were misleading. They didn't trigger before and after the entity had been persisted. Instead they triggered inside the CreateMedia method which never persists the entity. It constructs a new media object.

#### What do we use instead?

The MediaSavingNotification and MediaSavedNotification will always be published before and after an entity has been persisted. You can determine if an entity is brand new with either of those notifications. With the Saving notification - before the entity is persisted - you can check the entity's HasIdentity property which will be 'false' if it is brand new. In the Saved event you can [check to see if the entity 'remembers being dirty'](determining-new-entity.md)
