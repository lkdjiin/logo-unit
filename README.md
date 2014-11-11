Logo Unit Testing
=======================================================================

The `tt` procedure is a unit testing framework for the logo programming
language.

Getting Started
-----------------------------------------------------------------------

Say you want to write an `abs` procedure that returns the absolute value
of a number. `abs` will be in the file `math.lg`. Currently this procedure
doesn't exist.

Create a file for the tests, for example `test.math.lg`:

    $ ls
    math.lg
    test.math.lg

The first thing to do in `test.math.lg` is to load the source file:

```
load "math.lg
```

Now write your first test:

```
load "math.lg

to t.abs.outputs.a.number
assert.true number? abs 17
end
```

To run the test(s), open logo and call `tt` with the name of the test file:

    $ logo
    Welcome to Berkeley Logo version 5.5
    ? tt "test.math.lg
    I don't know how  to abs  in t.abs.outputs.a.number
    [assert.true number? abs 17]

The error message is clear: `abs` doesn't exist. So we create it in `math.lg`:

```
to abs :num
output :num
end
```

Relaunch the test:

    ? tt "test.math.lg
    .

    1 tests. 0 fail.
    ?

We did it!

Add a second test to deal with negative numbers:

```
to t.abs.outputs.the.right.value
assert.equal 17 abs -17
end
```

Test again:

    ? tt "test.math.lg
    .F
    t.abs.outputs.the.right.value
      expected: 17
      recieved: -17

    2 tests. 1 fail.
    ?

Fix it:

```
to abs :num
ifelse :num < 0 [output 0 - :num] [output :num]
end
```

And that's it.

    ? tt "test.math.lg
    ..

    2 tests. 0 fail.
    ?

Install
-----------------------------------------------------------------------

To install the `tt` procedure in UCBlogo, copy `tt.lg` in the folder of the
«logo standard library». In my debian box this is `/usr/share/ucblogo/logolib/`.


License
-----------------------------------------------------------------------

MIT.

TODO
--------

I didn't planned to make a procedure. What I originnaly wanted is a standalone
program, something like:

    $ logo-unit test.file.lg

**But**, I was not able to make the special variable `commandline` to work.

Test procedures
---------------

Name of test procedures **must** start with «t.», as in:

    t.this.should.do.that

As a convention, you should then give the tested procedure's name
and a short description of what is being tested. This is an example:

    to t.sum.outputs.a.number
    ; test
    end


Assertions
----------

### assert.array data

Assert that :date is an array.

### assert.equal expected value

Assert that :expected equals :value.

#### Example

    assert.equal [1 2] get.a.list

### assert.in list value

Assert that :value is a member of :list.

#### Example

    assert.in [1 2] get.a.value

### assert.list data

Assert that :data is a list.

### assert.number data

Assert that :data is a number.

### assert.true value

Assert that :value is "true.

#### Example

    assert.true number? :my.var

### assert.word data

Assert that :data is a word.


Special procedures
------------------

### before.all.test

If a procedure named «before.all.test» exists in a test file, it will
be ran one time, before the tests begin.
In this procedure you could setup often used values:

    to before.all.test
    make "t.value1 [0 1 2]
    make "t.value2 "foo
    end

You should prepend «t.» to your global variables…



Questions and/or Comments
-----------------------------------------------------------------------

Feel free to email [Xavier Nayrac](mailto:xavier.nayrac@gmail.com)
with any questions, or contact me on [twitter](https://twitter.com/lkdjiin).

