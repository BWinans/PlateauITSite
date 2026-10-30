# Contact Form

[← Previous: Deployment](02-deployment.md) · [Back to README](../README.md) · [Next: Customization →](04-customization.md)

The form on [`contact.html`](../contact.html) posts to `https://api.web3forms.com/submit`:

```html
<form id="contact-form" action="https://api.web3forms.com/submit" method="POST">
    <input type="hidden" name="access_key" value="...">
    <input type="hidden" name="subject" value="New Inquiry from PlateauIT.com">
    ...
    <div class="h-captcha" data-captcha="true" data-theme="dark"></div>
</form>

<script src="https://web3forms.com/client/script.js" async defer></script>
```

Submissions are emailed to the address associated with the Web3Forms access key.

## About the access key

Web3Forms access keys are designed to be public — they identify the destination inbox, not authorize an account. They are safe to commit. If the inbox changes or the key is abused, generate a new key in the Web3Forms dashboard and update the hidden input.

## hCaptcha

The form is protected by **hCaptcha**, using Web3Forms' zero-config integration — no hCaptcha account, site key, or secret key is required. Two pieces make it work:

1. The `<div class="h-captcha" data-captcha="true" data-theme="dark">` placeholder inside the form.
2. The `<script src="https://web3forms.com/client/script.js" async defer>` tag before `</body>`, which renders the widget and injects the `h-captcha-response` field.

An inline script also validates the challenge client-side before allowing submission:

```js
document.getElementById('contact-form').addEventListener('submit', function (e) {
    const hCaptchaResponse = this.querySelector('textarea[name="h-captcha-response"]');

    if (!hCaptchaResponse || !hCaptchaResponse.value.trim()) {
        e.preventDefault();
        alert('Please complete the captcha before submitting.');
    }
});
```

> **Required dashboard step:** hCaptcha must also be enabled for the form at [app.web3forms.com](https://app.web3forms.com) (open the form → spam protection settings → select hCaptcha). Without that, the widget renders but submissions are not actually verified.

`data-theme="dark"` matches the site's dark palette; other hCaptcha options can be passed as `data-*` attributes (for example `data-lang="es"` or `data-size="compact"`).

## Troubleshooting

| Symptom | Likely cause |
| --- | --- |
| Widget does not appear | Web3Forms client script blocked or not loaded |
| Widget appears but submissions fail | hCaptcha not enabled in the Web3Forms dashboard |
| "Please complete the captcha" alert loops | `h-captcha-response` field missing — check the client script tag |
| No email received | Wrong access key, or delivery filtered as spam |

---

[← Previous: Deployment](02-deployment.md) · [Back to README](../README.md) · [Next: Customization →](04-customization.md)
