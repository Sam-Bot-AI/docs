# Required informations
In order to integrate with Sam Bot you'll have to request for an `organizationId` and an `apiKey`.
## :office: Organization Id
Your organization Id will look like `sb-[16 characters]`. Eg:
```
sb-pfMOTn7lDnCsG2Pp
```
## :key: Api Key
Your organization Id will look like `sb-[32 characters]`. Eg:
```
sb-MwocWEq7mFXpfqCaxAQkF5ylonHIRv2g
```

# Integration Process
You would have to open a new window with our generated URL and pass some query string data along.
## Query string data
- `organizationId`: The organization Id we sent you.
- `apiKey`: The api key we sent you.
- `userId`: The id of the user accessing our application (this id is the id of your user from your application).
- `userEmail`: The email of the user accessing our application (this email is the email of your user from your application).
- `userName`: The name of the user accessing our application (this name is the name of your user from your application).
- `userPicture`: The picture of the user accessing our application (this picture is the picture of your user from your application).

Here is an example of a complete URL:
```
https://app.sam-bot.ai/chat-integration/auth?organizationId=[ORGANIZATION_ID]&apiKey=[API_KEY]&userId=[USER_ID]&userEmail=[USER_EMAIL]&userName=[USER_NAME]&userPicture=[USER_PICTURE]&
```
With this you're ready to go! :fire:

# Example of integrations
This is a JavaScript example as a reference but you should adapt this to your architecture.
## URL Generation
```js
const SAM_BOT_URL = 'https://app.sam-bot.ai';

interface Params {
  organizationId: string
  apiKey: string
  userId: string
  userEmail: string
  userName: string
  userPicture: string
}

const generateURL = ({
  organizationId,
  apiKey,
  userId,
  userEmail,
  userName,
  userPicture,
}: Params): string => `${SAM_BOT_URL}/chat-integration/auth?organizationId=${encodeURIComponent(organizationId)}&apiKey=${encodeURIComponent(apiKey)}&userId=${encodeURIComponent(userId)}&userEmail=${encodeURIComponent(userEmail)}&userName=${encodeURIComponent(userName)}&userPicture=${encodeURIComponent(userPicture)}`;
```
## Window opening
```js
interface Params {
  organizationId: string
  apiKey: string
  userId: string
  userEmail: string
  userName: string
  userPicture: string
}

const openWindow = ({
  organizationId,
  apiKey,
  userId,
  userEmail,
  userName,
  userPicture,
}: Params): void => {
  const heightThreshold = 650;
  const widthThreshold = 500;

  const outerWidth = window.outerWidth;
  const outerHeight = window.outerHeight;

  const left = outerWidth - widthThreshold > 0 ? (outerWidth - widthThreshold) / 2 : 0;
  const top = outerHeight - heightThreshold > 0 ? (outerHeight - heightThreshold) / 2 : 0;
  const width = outerWidth - widthThreshold > 0 ? widthThreshold : outerWidth;
  const height = outerHeight - heightThreshold > 0 ? heightThreshold : outerHeight;

  const url = generateURL(
    organizationId,
    apiKey,
    userId,
    userEmail,
    userName,
    userPicture,
  );

  window.open(url, '', `height=${height},width=${width},top=${top},left=${left}`);
};
```