---
title: "Demo Mermaid"
date: 2023-12-11T10:17:03+08:00
# bookComments: false
# bookSearchExclude: false
---

## Example

{{< columns >}}
```tpl
{{</*/* mermaid [class="text-center"]*/*/>}}
graph TD;
    R1[需求1:登录功能] -->F1((登录函数模块))
    R2[需求2:支付功能] --> F2((支付函数模块))
    R3[需求3:购物车功能] --> F3((购物车函数模块))
    R1 --> F4((Session管理模块))
    R2 --> F4
    F1 --> C1[登录页面组件]
    F1 --> C2[登录控制器]
    F2 --> C3[支付页面组件] 
    F2 --> C4[支付控制器]
    F3 --> C5[购物车页面组件]
    F3 --> C6[购物车控制器]
{{</*/* /mermaid */*/>}}
```

<--->

{{< mermaid >}}
graph TD;
    R1[需求1:登录功能] -->F1((登录函数模块))
    R2[需求2:支付功能] --> F2((支付函数模块))
    R3[需求3:购物车功能] --> F3((购物车函数模块))
    R1 --> F4((Session管理模块))
    R2 --> F4
    F1 --> C1[登录页面组件]
    F1 --> C2[登录控制器]
    F2 --> C3[支付页面组件] 
    F2 --> C4[支付控制器]
    F3 --> C5[购物车页面组件]
    F3 --> C6[购物车控制器]    
{{< /mermaid >}}

{{< /columns >}}

{{< columns >}}
```tpl
{{</*/* mermaid [class="text-center"]*/*/>}}
graph TD; 
    R1[需求1: 实现用户注册功能] --> F1[UserRegisterController]
    R1 --> F2[UserRegisterService]
    R1 --> F3[RegisterValidation]
    
    R2[需求2: 实现订单支付功能] --> F4[OrderPaymentController]
    R2 --> F5[PaymentService]
    R2 --> F6[PaymentValidation]
    
    R3[需求3: 实现商品收藏功能] --> F7[FavoriteController]
    R3 --> F8[FavoriteService]
    
    F1 --> C1[RegisterPage]
    F1 --> C2[RegisterAPI]
    F4 --> C3[PaymentPage]
    F4 --> C4[PaymentAPI]
    F7 --> C5[FavoritePage]
    
    C1[RegisterPage] --> D1[用户名输入框]
    C1 --> D2[密码输入框]
    C1 --> D3[注册按钮]
    
    C3[PaymentPage] --> D4[支付金额输入框]
    C3 --> D5[支付按钮]
{{</*/* /mermaid */*/>}}
```

<--->

{{< mermaid >}}
graph TD; 
    R1[需求1: 实现用户注册功能] --> F1[UserRegisterController]
    R1 --> F2[UserRegisterService]
    R1 --> F3[RegisterValidation]
    R2[需求2: 实现订单支付功能] --> F4[OrderPaymentController]
    R2 --> F5[PaymentService]
    R2 --> F6[PaymentValidation]
    R3[需求3: 实现商品收藏功能] --> F7[FavoriteController]
    R3 --> F8[FavoriteService]
    F1 --> C1[RegisterPage]
    F1 --> C2[RegisterAPI]
    F4 --> C3[PaymentPage]
    F4 --> C4[PaymentAPI]
    F7 --> C5[FavoritePage]
    C1[RegisterPage] --> D1[用户名输入框]
    C1 --> D2[密码输入框]
    C1 --> D3[注册按钮]
    C3[PaymentPage] --> D4[支付金额输入框]
    C3 --> D5[支付按钮]    
{{< /mermaid >}}

{{< /columns >}}



