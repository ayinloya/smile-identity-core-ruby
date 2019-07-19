# SmileIdentityCore

The official Smile Identity gem exposes two classes namely, the Web API and AuthSmile class.

The Web API allows you as the Partner to validate a user’s identity against the relevant Identity Authorities/Third Party databases that Smile Identity has access to using ID information provided by your customer/user (including photo for compare).

The Auth Smile class allows you as the Partner to generate a sec key to interact with our servers.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'smile-identity-core'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install smile-identity-core

## Usage


#### Calculating your Signature
```
$ connection = SmileIdentityCore::AuthSmile.new(partner_id, api_key)

$ sec_key = connection.generate_sec_key(timestamp)
where timestamp is optional

```

The response will be a hash:

```
{
  :sec_key=> "<the generated sec key>",
 :timestamp=> 1563283420
}
```

#### Web api
```
$ connection = SmileIdentityCore::WebApi.new(partner_id, default_callback, api_key, sid_server)

$ response = connection.submit_job(partner_params, images, optional_callback, return_job_status)
```

The response will be nil if you chose to set return_job_status to false, however if you have set return_job_status to true then you will receive a response like below:

```
{
  "timestamp": "2018-03-13T21:04:11.193Z",
  "signature": "<your signature>",
  "job_complete": true,
  "job_success": true,
  "result": {
    "ResultText": "Enroll User",
    "ResultType": "SAIA",
    "SmileJobID": "0000001897",
    "JSONVersion": "1.0.0",
    "IsFinalResult": "true",
    "PartnerParams": {
      "job_id": "52d0de86-be3b-4219-9e96-8195b0018944",
      "user_id": "e54e0e98-8b8c-4215-89f5-7f9ea42bf650",
      "job_type": 4
    },
    "ConfidenceValue": "100",
    "IsMachineResult": "true",
  }
  "code": "2302"
}
```
You can also view your response asynchronously at the callback that you have set, it will look as follows:
```
{
  "ResultCode": "1220",
  "ResultText": "Authenticated",
  "ResultType": "DIVA",
  "SmileJobID": "0000000001",
  "JSONVersion": "1.0.0",
  "IsFinalResult": "true",
  "PartnerParams": {
    "job_id": "e7ca3e6c-e527-7165-b0b5-b90db1276378",
    "user_id": "07a0c120-98d7-4fdc-bc62-3c6bfd16c60e",
    "job_type": 2
  },
  "ConfidenceValue": "100.000000",
  "IsMachineResult": "true"
}
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

Please note that you should tag the release when doing a push to rubygems.

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/smileidentity/smile-identity-core
