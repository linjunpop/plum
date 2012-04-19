---
layout: post
title: "Use Factory.stub to speedup Rspec test"
date: 2012-03-09 23:05
comments: true
categories: [rails, rspec, factory_girl]
---

In one of my company's recent project, the spec test become very slow.
After a research on that problem, I find a solution is to stub the
associated model in the model test.

Here is an example:

The `app/models/call_sheet.rb`:

```ruby
require 'spec_helper'

describe CallSheet do

  let(:call_sheet) { Factory(:call_sheet) }
  subject { call_sheet }

  describe 'associations' do
    it { should belong_to(:draft) }
    it { should belong_to(:category) }
    it { should belong_to(:stage) }
  end
end
```

Here is the `spec/support/factories/call_sheet.rb` factory:

```ruby
FactoryGirl.define do
  factory :call_sheet do
    company_name "the company"
    address "the address"
    association :draft
    association :stage
    association :category
  end
end
```

It's associate with `draft`, `stage` and `category`.

Now, run the spec test in my machine. Here's the result:

```ruby
Top 3 slowest examples:
  CallSheet associations 
    8.33 seconds ./spec/models/call_sheet_spec.rb:14
  CallSheet associations 
    7.42 seconds ./spec/models/call_sheet_spec.rb:16
  CallSheet associations 
    6.76 seconds ./spec/models/call_sheet_spec.rb:15

Finished in 22.51 seconds
```

It's very slow, because the `Draft`, `Stage`, `Category` is associate with other models too.
We should not care about that in the `CallSheet` model's rspec test.

So, I Changed `spec/models/call_sheet_spec.rb` to

```ruby
require 'spec_helper'

describe CallSheet do

  let(:project) { Factory.stub(:project) }
  let(:draft) { Factory.stub(:draft) }
  let(:stage) { Factory.stub(:stage) }
  let(:category) { Factory.stub(:category) }
  let(:call_sheet) { Factory(:call_sheet, draft: draft, stage: stage, category: category) }
  subject { call_sheet }

  describe 'associations' do
    it { should belong_to(:draft) }
    it { should belong_to(:category) }
    it { should belong_to(:stage) }
  end
end
```

The result:

```bash
Top 3 slowest examples:
  CallSheet associations 
    0.30077 seconds ./spec/models/call_sheet_spec.rb:13
  CallSheet associations 
    0.0172 seconds ./spec/models/call_sheet_spec.rb:15
  CallSheet associations 
    0.01644 seconds ./spec/models/call_sheet_spec.rb:14

Finished in 0.33607 seconds
```

Super fast now.
