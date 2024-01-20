---
weight: 999
title: "JS Functions"
description: ""
icon: "article"
date: "2023-10-27T20:42:12+02:00"
lastmod: "2023-10-27T20:42:12+02:00"
draft: false
toc: true
---

## actionFn

```js
const Dialog = ({ ... , actionFn, ... }) => {
    ...

    const onAction = (questionnaire, actionFn) => {
        (actionFn || _.identity)(questionnaire)
        close()
    }
    
    ...
    
    return <Button className='float-end' color='secondary'
                   onClick={ _.partial(onAction, questionnaire, actionFn) }>{ actionButtonLabel }</Button>
    ...
}
```





