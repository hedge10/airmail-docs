# Send messages

You can send requests either with content type `application/json` or with `application/x-www-form-urlencoded`. Other content types are not allowed and will return an error.

Depending on the content type, the notation of receivers, carbon copies (CC) or blind carbon copies (BCC) vary. There is no limit how many receivers, CC or BCC addresses you specify.

## Requests

### Fields

For detailed usage of these fields, f. ex setting multiple recipients, check out the examples below.

| Description                            | Type, Example                                  |  Field name      |
| -------------------------------------- | ---------------------------------------------- | :--------------- |
| Sender name                            | `string`,<br> Example: `John Doe`              | `sender-name`    |
| Sender addres                          | `string`,<br> Example: `john.doe@example.com`  | `sender-address` |
| Recipiens                              | `array`                                        | `to`             |
| Carbon copy                            | `array`                                        | `cc`             |
| Blind carbon copy                      | `array`                                        | `bcc`            |
| Subject                                | `string`                                       | `subject`        |
| Message                                | `string`                                       | `message`        |
| Define the content type of the message | `string`,<br> Example: `html` or `text`        | `_content-type`  |
| Redirect after sending                 | `string`,<br> Example: `https://www.dmain.com` | `_redirect`      |

### JSON request example

```shell
curl -X POST http://localhost:9900 \
  -H "Content-Type: application/json" \
  -d @- << EOF
{
    "sender-name": "John",
    "sender-address": "john.doe@example.com",
    "to": [
        {
            "name": "Batman & Robin",
            "address": "batman_and_robin@warnerbros.com"
        },
        {
            "name": "Mickey + Goofey",
            "address": "mickey_and_goofey@warnerbros.com"
        }
    ],
    "subject": "This is a marvelous email",
    "message": "This is some sample text.\r\nA new line is a good idea."
}
EOF
```

### Form request example

```shell
curl -X POST https://localhost:9900 \
   -H "Content-Type: application/x-www-form-urlencoded" \
   -d "sender-name=John Doe" \
   -d "sender-address=john.doe@example.de" \
   -d "to[0].name=Batman + Robin" \
   -d "to[0].address=batman_and_robin@warnerbros.com" \
   -d "to[1].name=Mickey + Goofey" \
   -d "to[1].address=mickey_and_goofey@warnerbros.com" \
   -d "subject=This is a marvelous email" \
   -d "message=My demo text" \
   -d "_content-type=html"
```

## Captcha validation

_Airmail_ supports the validation of [Google ReCaptcha](https://www.google.com/recaptcha/about/). For this to work, you need to define the environment variable `AM_GRECAPTCHA_SECRET` with the correct secret you got when setting up Google ReCaptcha.

Further your request needs to contain a field `g-recaptcha-response` holding the response you got back from Google. This is the default field name and should not be changed, as otherwise _Airmail_ cannot validate the request properly.

**Demo form**

Below is a demo form showing you how to integrate Google ReCaptcha. The captcha is built into a `div` container - `<div class="g-recaptcha" data-sitekey="<YOUR_SITE_KEY>"></div>`. Set the correct site key for the `data-sitekey` attribute before starting.

```html
<html>
  <head>
    <meta charset="UTF-8" />
    <script src="https://www.google.com/recaptcha/api.js" async defer></script>
  </head>
  <body>
    <div>
      <form name="demo-form" method="post" action="http://localhost:9900">
        <div>
          <div>
            <label for="sender-address">Sender</label>
            <input
              type="text"
              id="sender-address"
              name="sender-address"
              placeholder="Sender email"
              value="john.doe@example.com"
            />
          </div>
        </div>
        <div>
          <div>
            <label for="receiver-address1">Receiver</label>
            <input
              type="text"
              id="receiver-address1"
              name="to[0].address"
              value="receiver1@example.com"
            />
          </div>
        </div>
        <div>
          <input type="text" name="subject" id="subject" value="Test subject" />
        </div>
        <div>
          <textarea name="message" id="subject">My message...</textarea>
        </div>
        <div class="g-recaptcha" data-sitekey="<YOUR_SITE_KEY>"></div>
        <div>
          <button type="submit">Submit</button>
        </div>
      </form>
    </div>
  </body>
</html>
```

## Content type

Defining the content type of your message, aka MIME type, helps to correctly render the message content correctly, f. ex. links and formatting.

Set the `_content-type` parameter either to `text` or `html`.
