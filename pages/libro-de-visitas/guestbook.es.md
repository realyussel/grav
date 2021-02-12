---
title: guestbook.md
process:
    markdown: true
    twig: false
---

---
title: Guestbook

form:
    name: guestbook
    fields:

        - name: author
          label: Name
          placeholder: Enter your name
          autofocus: on
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          label: Email
          placeholder: Enter your email address
          type: email
          validate:
            required: true

        - name: text
          label: Message
          placeholder: Enter your message
          type: textarea
          validate:
            required: true

        - name: date
          type: hidden
          process:
            fillWithCurrentDateTime: true

        - name: g-recaptcha-response
          label: Captcha
          type: captcha
          recaptcha_site_key: 2jj21oiej23ioej23iojeoi32jeoi3
          recaptcha_not_validated: 'Captcha not valid!'
          validate:
            required: true
          process:
            ignore: true

    buttons:
        - type: submit
          value: Submit

    process:
        - captcha:
            recaptcha_secret: ej32uej3u2ijeiu32jeiu3jeuj32ui
        - email:
            subject: "[Site Guestbook] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            filename: messages.yaml
            operation: 'add'
        - message: Thank you for writing your message!
---

# Add message

### Enter your message: