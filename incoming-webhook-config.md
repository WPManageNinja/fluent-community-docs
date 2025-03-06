# Incoming Webhook in FluentCommunity

To connect with FluentCommunity with your external application, you can use the Incoming Webhook feature. This allows you to send messages to your FluentCommunity portal from any external application that supports webhooks.

## Creating an Incoming Webhook
1. Go to your FluentCommunity portal -> Settings -> Incoming Webhook.
2. Click Add New Webhook
3. Fill in the following fields:
   - **Name**: A name for your webhook.
   - **Add to Spaces**: Select the spaces those you want to add to the user when receiving the webhook.
   - **Remove from Spaces**: Select the spaces those you want to remove from the user when receiving the webhook.
   - **Add to Courses**: Select the courses those you want to add to the user when receiving the webhook.
   - **Remove from Courses**: Select the courses those you want to remove from the user when receiving the webhook.
   - If you want to send welcome email (WordPress Default) to the user, check the **Send Welcome Email** checkbox.
4. Click Save.

One you create the webhook, you will see a URL. This is the URL you will use to send payload to your FluentCommunity System. Please treat the webhook URL as your password.

## Sending Payload to FluentCommunity Webhook

To send payload to FluentCommunity webhook, you can use any HTTP client. Here is an example using `curl`:

You may send the Payload as Form Data and as a POST request.

```bash
curl --request POST \
  --url 'https://YOUR_WEBHOOK_URL' \
  --header 'Content-Type: multipart/form-data' \
  --header 'User-Agent: insomnia/8.6.1' \
  --form email=jewelssssss@gmail.com \
  --form first_name=FirstName \
  --form last_name=Lastname \
  --form user_login=user_login \
  --form user_pass=user_password
  ```

In this payload only email is required. 

## Payload Fields
| Field Name | Required | Description                                     |
|------------|----------|-------------------------------------------------|
| email | Yes | The email address of the user.                  |
| first_name | No | The first name of the user (For new user only). |
| last_name | No | The last name of the user (For new user only).  |
| user_login | No | The login name of the user (For new user only). |
| user_pass | No | The password of the user (For new user only).   |

If the user already exists, the webhook will use the user to assign the pre-configured courses and spaces. If the user does not exist, it will create a new user with the provided information.

