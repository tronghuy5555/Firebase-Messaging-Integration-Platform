
## Firebase-Messaging-Integration-Platform Mobile
[Firebase Messaging](https://firebase.flutter.dev/docs/messaging/overview/)
[Legacy FCM](https://firebase.google.com/docs/cloud-messaging/http-server-ref)
[Http v1 FCM](https://firebase.google.com/docs/cloud-messaging/migrate-v1)
### Note:
### Usecase 1: You want update badge count on app
iOS: Sever update badge in notification object, it will affect immediately
```json
{
  "notification": {
  	"title": "Title test",
  	"body": "Body test",
    "badge": 1

  },
  "data": {
    "title": "testing",
    "body": "body testing",
    "badge_count": 1,
    "click_action": "FLUTTER_NOTIFICATION_CLICK",
    "image": "https://znews-photo.zadn.vn/w1024/Uploaded/unvjuas/2019_11_28/EKd0aNJUUAAjsaH.jpeg",
    "noti_type": "comeent",
    "action": "today_mission_created",    
  },
  "to": "eFMTlzO"
}
```
Android: Sever need badge_count in data object, and Mobile side need update badge_count manually by using [flutter_app_badge](https://pub.dev/packages/flutter_app_badger) to update it
```dart
@pragma('vm:entry-point')
  static Future<void> firebaseMessagingBackgroundHandler(
      RemoteMessage message) async {
    // If you're going to use other Firebase services in the background, such as Firestore,
    // make sure you call `initializeApp` before using other Firebase services.
    await Firebase.initializeApp();
    final badgeCount = int.tryParse(message.data['badge_count'].toString());
          FlutterAppBadger.updateBadgeCount(badgeCount);
  }
```

