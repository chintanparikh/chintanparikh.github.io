---
layout: post
title: "Traits + Ignored Attributes = ♥"
date: 2013-06-05 21:22
comments: true
categories: 
---

If you don't know about FactoryGirl's traits, here's a quick primer:

They allow you to specify groups of attributes and callbacks that can be applied when you create the Factory in your tests. For example:

``` ruby A regular factory with a sub_referral
FactoryGirl.define do
  factory :referral do
    name 'A referral'
  	
    trait :with_sub_referrals do
  	  after(:create) do |referral|
        5.times { create(:sub_referral, referral: ref) }
  	  end
    end
  end
end
```

This lets you do something like

``` ruby
FactoryGirl.create(:referral, :with_sub_referrals)
```

But wait, I hear you say - why not just define a new factory, like so:

``` ruby A regular factory with a sub factory
FactoryGirl.define do
  factory :referral do
    name 'A referral'
  	
    factory :referral_with_sub_referrals do
  	  after(:create) do |referral|
  	    5.times { create(:sub_referral, referral: ref) }
  	  end
    end
  end
end
```

Sure, this works, but what if I have two traits?
``` ruby A regular factory with a sub_referral
FactoryGirl.define do
  factory :referral do
    name 'A referral'
  	
    trait :with_sub_referrals do
  	  after(:create) do |referral|
  	    5.times { create(:sub_referral, referral: ref) }
  	  end
    end
  	
    trait :with_rating do
  	  rating 5
    end
  end
end
```

Now, this lets you do
``` ruby
FactoryGirl.create(:referral, :with_sub_referrals, :with_rating)
```

Now you *could* do this by creating multiple factories, but it ends up remarkably ugly, and there's a tonne of code repetition (ew).

However, what if I want to specify how many sent_referrals I have in the above example. Unfortunately, you can't pass arguments into traits. Enter ignored attributes:

An ignored attribute is exactly what it sounds like - an attribute that's ignored when the object is created.

``` ruby A trait using ignored attributes
FactoryGirl.define do
  factory :referral do
    name 'A referral'
  	
    trait :with_sub_referrals do
  	  ignore do
  	    sent_referrals_count 5
  	  end
  	  
  	  after(:create) do |referral, eval|
  	    eval.sent_referral_count.times { create(:sub_referral, referral: ref) }
  	  end
    end
  	
    trait :with_rating do
  	  rating 5
    end
  end
end
```

So now, to set the number of sent_referrals that are created, I can do this:

``` ruby
FactoryGirl.create(:referral, :with_sent_referrals, sent_referral_count: 3)
```

Beautiful, isn't it?

