## Fix the Code
Suppose we are building a simple notification system for an app. 
We currently support three types of notifications: email, SMS, and push. 
Consider the following "Ugly Version":

```python
class EmailNotification:
    def __init__(self, address, subject, body):
        self.address = address
        self.subject = subject
        self.body = body

class SMSNotification:
    def __init__(self, phone_number, message):
        self.phone_number = phone_number
        self.message = message

class PushNotification:
    def __init__(self, device_id, title, message):
        self.device_id = device_id
        self.title = title
        self.message = message

def send_notification(notification):
    if isinstance(notification, EmailNotification):
        print(f"Sending EMAIL to {notification.address}")
        print(f"Subject: {notification.subject}")
        print(f"Body: {notification.body}")
    elif isinstance(notification, SMSNotification):
        print(f"Sending SMS to {notification.phone_number}")
        print(f"Message: {notification.message}")
    elif isinstance(notification, PushNotification):
        print(f"Sending PUSH to device {notification.device_id}")
        print(f"Title: {notification.title}")
        print(f"Message: {notification.message}")
    else:
        raise TypeError("Unsupported notification type")

notifications = [
    EmailNotification("alice@example.com", "Welcome!", "Thanks for signing up."),
    SMSNotification("+15551234567", "Your code is 1234"),
    PushNotification("device-xyz", "Update", "A new update is available."),
]

for n in notifications:
    send_notification(n)
```

### Task: Refactor Using Polymorphism

Refactor the design so that `send_notification` does not need to know the concrete types 
of the objects passed in and does not use `isinstance`.
