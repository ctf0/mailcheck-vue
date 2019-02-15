<h1 align="center" style="border: none">
    mailcheck-vue
    <br>
    <a href="https://www.npmjs.com/package/mailcheck-vue"><img src="https://img.shields.io/npm/v/mailcheck-vue.svg?style=for-the-badge" alt="npm" /></a> <a href="https://www.npmjs.com/package/mailcheck-vue"><img src="https://img.shields.io/npm/dt/mailcheck-vue.svg?style=for-the-badge" alt="npm" /></a>
</h1>

## Installation

```bash
npm install mailcheck-vue --save
```

## Usage

- register the component

    ```js
    window.Vue = require('vue')

    Vue.component('MailCheck', require('mailcheck-vue').default)
    ```

- now use it like
    ```html
    <mail-check
        model-name="email"
        :data="email"
        :domains="['gmail.com', 'aol.com']"
        :topLevelDomains="['com', 'net', 'org']"
        :secondLevelDomains="['hotmail']"
        :distanceFunction="someFunction">

        <span>Did you Mean</span>
    </mail-check>
    ```

    |        prop        |      required      |   type   |           default            |                description                |
    |--------------------|--------------------|----------|------------------------------|-------------------------------------------|
    | modelName          | :white_check_mark: | string   |                              | the v-model key we should update on click |
    | data               | :white_check_mark: | string   |                              | the v-model value we want to check        |
    | domains            | :x:                | array    | Mailcheck.domains            | [mailcheck][docs]                         |
    | topLevelDomains    | :x:                | array    | Mailcheck.topLevelDomains    | [mailcheck][docs]                         |
    | secondLevelDomains | :x:                | array    | Mailcheck.secondLevelDomains | [mailcheck][docs]                         |
    | distanceFunction   | :x:                | function | Mailcheck.sift4Distance      | [mailcheck][docs]                         |

[docs]: https://github.com/mailcheck/mailcheck/blob/master/src/mailcheck.js

> \# Why we need both `data` & `modelName` ? <br>
> to update the parent v-model without the need to use an EventBus, if someone have a better idea am all :ear:.

- to style the result, use `mail-check` ex.
    ```css
    .mail-check {
        cursor: pointer;
        color: red;
    }
    ```
