---
layout: post
title: 'Build a SAAS App with Flask: Part 3'
tags: [flask, bsawf, tutorial]
excerpt:
  Learn about the Build a SAAS App with Flask project, this is part 3 of a 5
  part series.
---

The source code can be found here:  
[http://github.com/nickjj/build-a-saas-app-with-flask](http://github.com/nickjj/build-a-saas-app-with-flask)

#### Looking for the other parts of this series?

- [Part 1]({% post_url 2015-05-20-build-a-saas-app-with-flask-part-1 %})
- [Part 2]({% post_url 2015-05-23-build-a-saas-app-with-flask-part-2 %})
- Part 3
- [Part 4]({% post_url 2015-06-05-build-a-saas-app-with-flask-part-4 %})
- [Part 5]({% post_url 2015-06-24-build-a-saas-app-with-flask-part-5 %})

### What's been added since the second part?

The entire billing component! Here's some of the features:

![Process payment]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-process-payment.jpg "Process payment")

#### Subscription

- Easily add, delete or sync your custom plans with a payment gateway
- Users can pick a plan from a pricing table
- Users can upgrade, downgrade or cancel their subscription

![Change plans]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-change-plans.jpg "Change plans")

- Users can update their billing information
- Users can view their billing details and upcoming payments

![Subscription details]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-subscription-details.jpg "Subscription details")

- Users can apply coupons to their subscription

#### Credit card

- Track when credit cards are about to expire
- Notify users when their card is about to expire

![Expiring card]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-expiring-card.jpg "Expiring card")

#### Coupons

- Coupons can be percent based or a fixed amount
- Coupons can expire after a certain time
- Coupons can have a max redemption attribute attached to them
- Coupons can be randomly generated with human friendly codes
- Coupons can be applied to new or existing subscriptions
- Keep track of how often a coupon was used

![Manage coupons]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-manage-coupons.jpg "Manage coupons")

#### Admin dashboard

- Coupons can be managed through the dashboard
- View any user's subscription details
- Cancel any user's subscription
- Dashboard stats related to billing

![User subscription details]({{ site.baseurl}}assets/img/blog/build-a-saas-app-with-flask-v1-user-subscription-details.jpg "User subscription details")

### On the horizon

A better test strategy and lots more tests for all of the billing components. We
will be mocking out the payment gateway APIs but do end to end tests on our SAAS
app.
