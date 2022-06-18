# Module Development

- powerfull way to reuse code
- write module yourself
- https://registry.terraform.io/namespaces/terraform-aws-modules
- https://github.com/orgs/terraform-aws-modules/repositories
- module can be fetched from github

```
module "my-service" {
  source = "github.com/<your modules file>"
}
```

- https://github.com/wardviaene/terraform-course/tree/master/module-demo
