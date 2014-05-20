* Annotations should usually be written on the line immediately above
  the relevant code.

* The annotation keyword is followed by a colon and a space, then a note
  describing the problem.

* If multiple lines are required to describe the problem, subsequent
  lines should be indented two spaces after the `#`.

  ```Ruby
  def bar
    # FIXME: This has crashed occasionally since v3.2.1. It may
    #   be related to the BarBazUtil upgrade.
    baz(:quux)
  end
  ```

* In cases where the problem is so obvious that any documentation would
  be redundant, annotations may be left at the end of the offending line
  with no note. This usage should be the exception and not the rule.

  ```Ruby
  def bar
    sleep 100 # OPTIMIZE
  end
  ```

* Use `TODO` to note missing features or functionality that should be
  added at a later date.

* Use `FIXME` to note broken code that needs to be fixed.

* Use `OPTIMIZE` to note slow or inefficient code that may cause
  performance problems.

* Use `HACK` to note code smells where questionable coding practices
  were used and should be refactored away.

* Use `REVIEW` to note anything that should be looked at to confirm it
  is working as intended. For example: `REVIEW: Are we sure this is how the
  client does X currently?`

* Use other custom annotation keywords if it feels appropriate, but be
  sure to document them in your project's `README` or similar.

