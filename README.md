# Karla

[![All Tests](https://github.com/McPringle/karla/actions/workflows/all-tests.yml/badge.svg)](https://github.com/McPringle/karla/actions/workflows/all-tests.yml)

**The Magazin Manager**

The name *Karla* is based on the fictional character Karla Kolumna from the well-known children's radio plays about the elephant Benjamin Blümchen. Karla is the roving reporter from Neustadt. She is constantly on the lookout for news and “sensational” stories on her scooter.

## Build

### Maven

*Karla* uses [Maven](https://maven.apache.org/) to build the project. Please use standard Maven commands to build what you need:

| Command          | What it does                                                      |
|------------------|-------------------------------------------------------------------|
| `./mvnw`         | compile and run the app                                           |
| `./mvnw clean`   | cleanup generated files and build artefacts                       |
| `./mvnw compile` | compile the code without running the tests                        |
| `./mvnw test`    | compile and run all tests                                         |
| `./mvnw package` | compile, test, and create a JAR file to run it with Java directly |
| `./mvnw verify`  | compile, test, package, and run analysis tools                    |

There is *no need* to run the `install` or `deploy` tasks. They will just run longer, produce unnecessary output, burn energy, and occupy your disk space. [Don't just blindly run mvn clean install...](https://www.andreaseisele.com/posts/mvn-clean-install/)

### Docker

*Karla* comes with a complete dockerized build for production use. It is not recommended to use the self-contained build for development purposes. Please take a look at the section about [Production Build](#production-build) below.

## Running and debugging

### Running from the command line

To run from the command line, run `./mvnw` and open [http://localhost:8080](http://localhost:8080) in your browser.

### Running and debugging in Intellij IDEA

- Locate the `Application.java` class in the project view. It is in the `src` folder, under the main package's root.
- Right-click on the `Application` class
- Select "Debug 'Application.main()'" from the list

After the server has started, you can view the UI at [http://localhost:8080](http://localhost:8080) in your browser.
You can now also attach breakpoints in code for debugging purposes, by clicking next to a line number in any source file.

### Running and debugging in Eclipse

- Locate the `Application.java` class in the package explorer. It is in `src/main/java`, under the main package.
- Right-click on the file and select `Debug As` --> `Java Application`.

Do not worry if the debugger breaks at a `SilentExitException`. This is a Spring Boot feature and happens on every startup.

After the server has started, you can view it at [http://localhost:8080](http://localhost:8080) in your browser.
You can now also attach breakpoints in code for debugging purposes, by clicking next to a line number in any source file.

## Configuration

*Karla* can be started without any specific configuration. All configuration options have working default values.

### Configuration Options

To modify the default configuration values, just specify environment variables with the following names:

| Environment Variable       | Default | Description                                                                  |
|----------------------------|---------|------------------------------------------------------------------------------|
| TZ                         | UTC     | The timezone used for date and time calculations.                            |

## Production

### Production Build

#### Maven

You can use [Maven](https://maven.apache.org/) to build *Karla* for production. Just specify the `production` profile. Example:

```shell
./mvnw clean package -Pproduction
```

#### Docker

To create a production build for *Karla* it is highly recommended to use [Docker](https://www.docker.com/) or [Podman](https://podman.io/). *Karla* comes with a complete dockerized self-contained build. You don't need to have Maven or Java installed, [Docker](https://www.docker.com/) or [Podman](https://podman.io/) is enough. The Docker build file contains everything needed, just start a standard Docker build with the following command:

```shell
docker build -t karla .
```

This might run for a while and will produce a Docker image tagged `karla` on your local system.

### Run in Production

It is highly recommended to use [Docker](https://www.docker.com/) or [Podman](https://podman.io/) to run *Karla* in production. Use the following command line as an example:

```shell
docker run \
    --name karla \
    -p 80:8080 \
    -e TZ=CET \
    -d \
    --rm \
    mcpringle/karla
```

Short explanation, consult the Docker or Podman documentation for more information about all available options for running an image.

| Option          | Explanation                                    |
|-----------------|------------------------------------------------|
| --name karla    | Specify the name for the running instance.     |
| -p 80:8080      | Make *Karla* available on host port 80         |
| -e KEY=value    | Configure *Karla* using environment variables. |
| -d              | Run *Karla* in daemon mode (background).       |
| --rm            | Remove the container when stopping *Karla*.    |
| mcpringle/karla | The Docker image to be started.                |

Modify this command according your needs and consult the [configuration section](#configuration) above for more information about how to configure *Karla*. The Docker image of *Karla* will be pulled from [Docker Hub](https://hub.docker.com/) automatically when not available locally.

## Communication

### Matrix Chat

There is a channel at Matrix for quick and easy communication. This is publicly accessible for everyone. For developers as well as users. The communication in this chat is to be regarded as short-lived and has no documentary character.

You can find our Matrix channel here: [@project-karla:ijug.eu](https://matrix.to/#/%23project-karla:ijug.eu)

### GitHub Discussions

We use the corresponding GitHub function for discussions. The discussions held here are long-lived and divided into categories for the sake of clarity. One important category, for example, is that for questions and answers.

- [Discussions on GitHub](https://github.com/McPringle/karla/discussions)
- [Questions and Answers](https://github.com/McPringle/karla/discussions/categories/q-a)

## Contributing

### Good First Issues

To find possible tasks for your first contribution to *Karla*, we tagged some of the hopefully easier to solve issues as [good first issue](https://github.com/McPringle/karla/labels/good%20first%20issue).

If you prefer to meet people in real life to contribute to *Karla* together, we recommend to visit a [Hackergarten](https://www.hackergarten.net/) event. *Karla* is often selected as a contribution target in [Lucerne](https://www.meetup.com/hackergarten-luzern/) and [Zurich](https://www.meetup.com/hackergarten-zurich/).

Please join our developer community using our [Matrix chat](#matrix-chat) to get support and help for contributing to *Karla*.

### Sign-off your commits

It is important to sign-off *every* commit. That is a de facto standard way to ensure that *you* have the right to submit your content and that you agree to the [DCO](DCO.md) (Developer Certificate of Origin).

You can find more information about why this is important and how to do it easily in a very good [blog post](https://dev.to/janderssonse/git-signoff-and-signing-like-a-champ-41f3) by Josef Andersson.

### Add an emoji to your commit

We love to add an emoji to the beginning of every commit message which relates to the nature of the change. You can find a searchable list of possible emojis and their meaning in the overview on the [gitmoji](https://gitmoji.dev/) website. If you prefer, you can also install one of the plugins that are available for almost all common IDEs.

### AI Generated Code

AI generated source code is based on real existing source code, which is copied in whole or in part into the generated code. The license of the original source code with which the AI was trained is not taken into account. It is not clear which license conditions apply and how these can be complied with. For legal reasons, we therefore do not allow AI-generated source code at all.

## Contributors

Special thanks for all these wonderful people who had helped this project so far ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/McPringle"><img src="https://avatars.githubusercontent.com/u/1254039?v=4?s=100" width="100px;" alt="Marcus Fihlon"/><br /><sub><b>Marcus Fihlon</b></sub></a><br /><a href="#projectManagement-McPringle" title="Project Management">📆</a> <a href="#ideas-McPringle" title="Ideas, Planning, & Feedback">🤔</a> <a href="https://github.com/McPringle/karla/commits?author=McPringle" title="Code">💻</a> <a href="#design-McPringle" title="Design">🎨</a></td>
      <td align="center" valign="top" width="14.28%"></td>
      <td align="center" valign="top" width="14.28%"></td>
      <td align="center" valign="top" width="14.28%"></td>
      <td align="center" valign="top" width="14.28%"></td>
      <td align="center" valign="top" width="14.28%"></td>
      <td align="center" valign="top" width="14.28%"></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

## Copyright and License

[AGPL License](https://www.gnu.org/licenses/agpl-3.0.de.html)

*Copyright (C) Marcus Fihlon and the individual contributors to **Karla**.*

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.
