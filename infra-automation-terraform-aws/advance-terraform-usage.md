# Advanced Terraform Usages

## Interpolation

- Interpolate other value with `${...}`
- Simple math function, conditional if-else

- `lookup()` to lookup map
- `join()` to join a list
- `module.NAME.output`, to output module
- `count.FIELD` 
- `path.TYPE` (path.cwd) (path.module) (path.root)
- `terraform.FIELD`

You can use simple math in interpolation `${2 + 2 / 4}`

## Conditionals

```
"${var.env == "prod" ? 2 : 1}"
```

Support all compare operator like cpp

https://github.com/wardviaene/terraform-course/tree/master/demo-18

## Built in functions

Terraform functions built in functions

https://www.terraform.io/language/functions

## For and for each loop

https://www.terraform.io/language/meta-arguments/for_each

## Terraform project structure

- Its best to have `development` and `production` terraform settings
- Typically you'll be better to have 3 different aws account, prod, dev, and billing
- Separate as module
- Separate vpc dev and prod too

https://github.com/wardviaene/terraform-course/tree/master/demo-18b

## Terraform lock file

- Tracks the versions of providers and modules
- Lockfile should be committed to git
- Terraform will make change to the lock file if requirements changed


## Manipulating state

https://www.terraform.io/cli/state

