---
title: Contact
body_classes: uk-container-xsmall uk-align-center
hero: true
form:
    name: contact-form
    fields:
        - name: name
          label: Name
          placeholder: Enter your name
          autofocus: on
          autocomplete: on
          type: text
          validate:
            required: true
          classes: uk-input uk-margin-bottom
          labelclasses: uk-form-label

        - type: spacer
          title: Contact Information
          classes: uk-margin-top

        - name: honeypot
          type: honeypot

        - name: email
          label: Email
          placeholder: Enter your email address
          type: email
          validate:
            required: true
          classes: uk-input uk-margin-bottom
          labelclasses: uk-form-label

        - name: phone
          label: Phone
          placeholder: 123-456-7890
          type: tel
          validate:
            required: false
          classes: uk-input uk-margin-bottom
          labelclasses: uk-form-label

        - type: spacer
          title: Trip dates
          classes: uk-margin-top

        - name: start-date
          type: date
          label: from:
          size: x-small
          validate.min: "2019-01-01"
          validate.max: "2050-12-31"
          validate:
            required: false
          classes: uk-input uk-margin-bottom
          labelclasses: uk-form-label

        - name: end-date
          type: date
          label: to:
          size: x-small
          validate.min: "2019-01-01"
          validate.max: "2050-12-31"
          validate:
            required: false
          classes: uk-input uk-margin-bottom
          labelclasses: uk-form-label

        - type: spacer
          title: Your message
          classes: uk-margin-top

        - name: message
          label: Message
          placeholder: Get in touch...
          type: textarea
          validate:
            required: true
          classes: uk-textarea uk-margin-bottom
          labelclasses: uk-form-label

    buttons:
        - type: submit
          value: Submit
          classes: uk-button uk-button-primary
        - type: reset
          value: Reset
          classes: uk-button uk-button-default

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.to }}"
              - "{{ form.value.email }}"
            reply_to: “{{ form.value.email }}”
            subject: "[Web contact] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Thank you for getting in touch!
        - display: thankyou

---
