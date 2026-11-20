# domain-supervisor

Run a co-routine inside a Node `domain` and restart it when it throws, so one bad worker cannot take down the whole process.

> **Status: dormant since 2014.** A small library Steven Zeiler wrote in November and December 2014, inspired by Erlang's Supervisor and Process. It has had no changes since 2014-12-17. Node's `domain` module is documented as deprecated, so treat this as a reference or a starting point, not a production dependency.

## Install

    npm install domain-supervisor

(The package was never confirmed as published from this repo; if the install fails, install from GitHub: `npm install stevenzeiler/domain-supervisor`.)

## Usage

    var Supervisor = require('domain-supervisor').Supervisor;
    var Process = require('domain-supervisor').Process;

    var proc = new Process(myCoRoutine);
    var supervisor = new Supervisor();

    supervisor.run(proc, function(error, restart, crash) {
      console.log('Handling error:', error.stack);
      restart();            // run the co-routine again
      // crash(error);      // or rethrow, if you do want the process to die
    });

    function myCoRoutine() {
      setInterval(function() {
        throw new Error('some terrible exception!');
      }, 1000);
    }

## Configuration

None. There are no environment variables.

## How it works

- `Process` wraps a function (`new Process(fn)`); `fn` is called as `proc.start()`.
- `Supervisor.run(proc, onError)` creates a `domain`, runs the process inside it, and listens for the domain's `error` event.
- `onError(error, restart, crash)` is called on each uncaught exception. `restart()` runs the process again in the same domain. `crash(error)` rethrows.

The code is about 25 lines in `src/supervisor.js` and `src/process.js`.

## Tests

    npm test

This runs `node test/`, a script (not a test framework) that lets a process fail three times, restarts it each time, and on the fourth error calls `crash` on purpose. A non-zero exit and a stack trace at the end are the expected result.

## Status

See [docs/STATUS.md](docs/STATUS.md). License: ISC (see [LICENSE](LICENSE)).
