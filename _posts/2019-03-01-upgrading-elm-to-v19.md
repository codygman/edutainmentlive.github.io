# Upgrading Elm from 0.18 to 0.19

by The Engineering Team

[Elm](https://elm-lang.org/) is a front-end, functional language that compiles to JavaScript for
seamless web development, and we love it. It's been around for years, and in August of 2018 it
upgraded to version 0.19. We didn't get around to upgrading our app to 0.19 until January of 2019.

The creator of Elm released [this upgrade
guide](https://github.com/elm/compiler/blob/a968e817e65d30493c344ac96c9c904b19a7f038/upgrade-docs/0.19.md)
as well as [this document about what
changed](https://elm-lang.org/blog/small-assets-without-the-headache), both were helpful but neither
was an end-all answer. In this post, we will go over what didn't go well for us, changes we as a
team would suggest, and the wonderful things about Elm 0.19 that make this upgrade worth the
potential struggle.

## What Didn't Go Well For Us

1. Several breaking changes
   1. elm-lang/core/Date became elm/Time/Posix, but it doesn't quite have all the same functionality
      and, notably, is no longer in core.
   1. Navigation changed. From the docs, 'A navigation Key is needed to create navigation commands
      that change the URL, including back and forward.'
   1. HTTP library. We really liked these changes but this package felt like it had more breaking
      changes than any other package for us.
   1. Various function signatures changed, some without obvious benefit. We're giving the Elm
      maintainers the benefit of the doubt because they've made a great language and they're
      probably way smarter than us, so there's probably good reason for the change, but we would have
      preferred more explanation to these changes.
1. With breaking changes comes a broken compiler, which would not be revived until dependencies were
   sorted through. This is especially noticeable with Elm, whose compiler is very friendly and
   helpful, so not having it available was both obvious and painful. While that does make some
   sense since the compiler was updated in tandem, having a working compiler to guide us through
   how to use new dependencies would have been helpful in more efficiently figuring out what was broken.
1. The old documentation became tough to find - the 0.19 documents replaced 0.18 on elm-lang, and
   after some digging we were able to find a Github site that contained their (hopefully permanent)
   location [here](https://dmy.github.io/elm-0.18-packages/). It was good they were somewhere, but some
   link between 0.19 and 0.18 would have been helpful.
1. Some elm-community packages were no longer supported, and we chose those over others specifically
   because they were elm-community and were more likely to be supported, integrated, or at least
   easy to update; however, they didn't all make it into 0.19 which felt very disappointing.
1. We had to fork and upgrade some dependencies because it was easier to upgrade them than to choose
   another dependency, namely [elm-bootstrap](https://github.com/rundis/elm-bootstrap) and
   [elm-dropdown](https://github.com/sporto/elm-dropdown). Not really the fault of Evan and Co., but
   since it was something we had to handle, we've added it to this section.

## Potential Upgrade Changes

1. As noted, having a working compiler, especially elm's friendly compiler, makes working through
   kinks much easier. With 0.19, the compiler and packages have to be upgraded simultaneously. If
   these were separate, allowing for one to be upgraded at a time, the upgrade process would be much
   smoother in both scenarios.
1. While breaking changes can be necessary, it would be nice to have a bridge in-between in order to
   help acclimate to a breaking change - for example, introducing breaking changes but allowing for
   compiler compatibility in an 0.18.5 version in order to make the change over from 0.18 to 0.19
   smoother.
1. Make previous versions' documentation easier to find, and make it easier to compare with the new
   version. This is super helpful when type signatures change. A lot of the documentation available
   for other languages allows a user to select versions to look at in order to compare between
   versions.

## What We Like about 0.19

1. More elm/ packages, such as browser, json, svg, time, and url. We love having elm/ packages,
   because they are more likely to be kept up by the community and integrated into future Elm
   upgrades.
1. Removed polymorphic `toString` function, which was replaced by Int.toString. This is safer.
1. Documentation is better. It looks like Evan and Co. tried really hard to improve the examples to
   make them shorter and clearer wherever possible.
1. HTTP package got markedly better with functions  like `riskyRequest` and `riskyTask` functions so
   you _know_ you're using risky security policies, and the function signatures for `post` and `get`
   got better.
