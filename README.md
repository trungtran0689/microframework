# MicroFramework

Micro framework integrates popular libraries like [express.js][1], [Mongodb ODM][2], [validator.ts][5],
[controllers.ts][4], [event-dispatcher.ts][7]
and others for use in your Typescript application. Framework ships by default [dependency injection framework][3] and
[configuration framework][6] to make all modules to work like a sh

## Notice

Library is under active development and API may change from version to version. 
Please consider it before using this library.

## Installation

You use framework with one or more the available modules. Lets say you want to use [express.js][1], [Mongodb ODM][2],
[validator][5], [event-dispatcher][7] and [restful controllers][4].

1. Install npm modules: 

`npm install microframework microframework-express microframework-typeodm microframework-controllers.ts
microframework-validator.ts microframework-event-dispatcher.ts microframework-configurator.ts
configurator.ts controllers.ts typedi typeodm validator.ts --save`

2. Install required tsd dependencies:

`tsd install es6-promise express mongodb --save`

4. Link definitions of the installed npm modules:

    `tsd link`

## Usage

1. Create `app.ts`:
    
    ```typescript
    import {MicroFrameworkBootstrapper} from "microframework/MicroFrameworkBootstrapper";
    import {ExpressModule} from "microframework-express/ExpressModule";
    import {ControllersTsModule} from "microframework-controllers.ts/ControllersTsModule";
    import {TypeOdmModule} from "microframework-typeodm/TypeOdmModule";
    import {ValidatorTsModule} from "microframework-validator.ts/ValidatorTsModule";
    import {EventDispatcherTsModule} from "microframework-event-dispatcher.ts/EventDispatcherTsModule";
    
    new MicroFrameworkBootstrapper({ srcDirectory: __dirname })
        .registerModules([
            new ExpressModule(),
            new TypeOdmModule(),
            new ControllersTsModule(),
            new ValidatorTsModule(),
            new EventDispatcherTsModule()
        ])
        .bootstrap()
        .then(result => console.log('Module is running. Open localhost:3000'))
        .catch(error => console.error('Error: ', error));
    ```
    
2. Create configuration file `configuration/config.json`:
    
    ```json
    {
      "express": {
        "port": "3000",
        "bodyParser": {
            "type": "json"
        }
      },
      "typeodm": {
        "connection": {
          "url": "mongodb://localhost:27017/microframework-sample"
        }
      }
    }
    ```
    
3. Now create your first controller, lets say QuestionController: `controller/QuestionController.ts`:
    
    ```typescript
    import {JsonController, Get} from "controllers.ts/Annotations";
    import {Response, Request} from "express";

    @JsonController()
    export class QuestionController {
    
        @Get('/questions')
        all(): any[] {
            return [
                { title: 'Which processor to choose?', text: 'Which processor is better: Core i5 or Core i7?' },
                { title: 'When new star wars gonna be released?', text: 'When star wars gonna be released? I think in december' }
            ];
        }
    }
    ```

4. Run your app and open `http://localhost:3000/questions` in browser. You should see list of your questions.

## Available Modules

* [microframework-express](https://github.com/PLEEROCK/microframework-express) - integration with [express.js][1]
* [microframework-typeodm](https://github.com/PLEEROCK/microframework-typeodm) - integration with [TypeODM][2]
* [microframework-controllers.ts](https://github.com/PLEEROCK/microframework-controllers.ts) - integration with [controllers.ts][4]
* [microframework-validator.ts](https://github.com/PLEEROCK/microframework-validator.ts) - integration with [validator.ts][5]
* [microframework-event-dispatcher.ts](https://github.com/PLEEROCK/microframework-event-dispatcher.ts) - integration with [event-dispatcher.ts][7]
* [microframework-winston](https://github.com/PLEEROCK/microframework-winston) - integration with [winston][8]
* [microframework-elasticsearch](https://github.com/PLEEROCK/microframework-elasticsearch) - integration with [elasticsearch][9]
* [microframework-rabbit.ts](https://github.com/PLEEROCK/microframework-rabbit.ts) - integration with [rabbit.js][10]
* [microframework-event-dispatcher.ts](https://github.com/PLEEROCK/microframework-event-dispatcher.ts) - integration with [event-dispatcher.ts][11]

## Todos

* cover with tests
* more documentation and examples
* more modules

[1]: http://expressjs.com/
[2]: https://github.com/PLEEROCK/typeodm
[3]: https://github.com/PLEEROCK/typedi
[4]: https://github.com/PLEEROCK/controllers.ts
[5]: https://github.com/PLEEROCK/validator.ts
[6]: https://github.com/PLEEROCK/configurator.ts
[7]: https://github.com/PLEEROCK/event-dispatcher.ts
[8]: https://github.com/winstonjs/winston
[9]: https://github.com/elastic/elasticsearch-js
[10]: https://github.com/squaremo/rabbit.js/
[11]: https://github.com/PLEEROCK/event-dispatcher.ts
