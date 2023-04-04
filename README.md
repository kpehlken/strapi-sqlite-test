# 🚀 Getting started with Strapi

## 📜 Contents

1. Official: Strapi getting started
2. Internal: Strapi workflow

---

## 🚀 1. Official: Strapi getting started

Strapi comes with a full featured [Command Line Interface](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html) (CLI) which lets you scaffold and manage your project in seconds.

### `develop`

Start your Strapi application with autoReload enabled. [Learn more](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html#strapi-develop)

```
yarn develop
```

### `start`

Start your Strapi application with autoReload disabled. [Learn more](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html#strapi-start)

```
yarn start
```

### `build`

Build your admin panel. [Learn more](https://docs.strapi.io/developer-docs/latest/developer-resources/cli/CLI.html#strapi-build)

```
yarn build
```

## ⚙️ Deployment

Strapi gives you many possible deployment options for your project. Find the one that suits you on the [deployment section of the documentation](https://docs.strapi.io/developer-docs/latest/setup-deployment-guides/deployment.html).

## 📚 Learn more

- [Resource center](https://strapi.io/resource-center) - Strapi resource center.
- [Strapi documentation](https://docs.strapi.io) - Official Strapi documentation.
- [Strapi tutorials](https://strapi.io/tutorials) - List of tutorials made by the core team and the community.
- [Strapi blog](https://docs.strapi.io) - Official Strapi blog containing articles made by the Strapi team and the community.
- [Changelog](https://strapi.io/changelog) - Find out about the Strapi product updates, new features and general improvements.

Feel free to check out the [Strapi GitHub repository](https://github.com/strapi/strapi). Your feedback and contributions are welcome!

## ✨ Community

- [Discord](https://discord.strapi.io) - Come chat with the Strapi community including the core team.
- [Forum](https://forum.strapi.io/) - Place to discuss, ask questions and find answers, show your Strapi project and get feedback or just talk with other Community members.
- [Awesome Strapi](https://github.com/strapi/awesome-strapi) - A curated list of awesome things related to Strapi.

---

## 2. ⚒️ Internal: Strapi workflow

### Situation and Strategy

When developing Strapi locally each local instance will have its own database. With multiple local development environments the synchronisation of Strapis state must be achieved, progressevely taken care of and ensured.

Since Strapi v4.6 a native [import/export-functionality](https://docs.strapi.io/developer-docs/latest/developer-resources/data-management.html) has been implemented. This allows for the export of the database (including relations and files) as well as the import of such an exported state.

> _**The catch:**_ When importing a database, the existing database will be deleted completely. Fusion like with solving merge conflicts is not possible. This means:
>
> - There can only be one true database (State of Strapi) at a time
> - When updating Strapi (e. g. adding Content Types and Components or changing data such as test or images), this new state must be exported and distributed to all environments.
> - _**Before**_ updating Strapi it must be ensured that this can happen properly: so working branches must be merged or every environment must receive the current import/export archive and import it.
> - A backup file must be saved in a secure place along with all the previous import-export files
>   > The name of each file contains a timestamp (yyyy-mm-dd + increment in vX-format), for example: `Ankerland-Export-2023-02-15-v2.tar.gz`
> - The updating of Strapi can only happen in one environment. Or step by step over multiple environments. However, the development process must halt for that time
>   > _**In short:**_
>   >
>   > 1.  Make sure, a Strapi structure update can happen without conflicts (e. g. merge branches if neccessary, or put update on hold until other work is completed)
>   > 2.  Take care of the update in one place and in one chunk – hold all conflicting processes
>   >     - prefix commit message with an all capital `STRAPI`
>   > 3.  Apply the update to all environments
>   > 4.  Add the update to the backup history
>   > 5.  Continue with frontend development ✨

> Always plan the update with everyone involved who could affect or be affected by the process 🤗.

</br>

### CLI execution

Navigate into the `cms` directory:

```bash
cd cms
```

There is a directory called `strapi export` with an archive named `Ankerland-Export.tar.gz`. If you pulled the changes, you import that file from that directory. If you did the changes you export that file to that directory. The process is conveniently handled by two scripts you can execute within the `cms` directory.

Import database:

```bash
yarn db-import
```

Export database:

```bash
yarn db-export
```

These scripts make use of the Strapi CLI and respectively point to

```bash
strapi export --no-encrypt -f strapi-export/Ankerland-Export
```

or

```bash
strapi import -f strapi-export/Ankerland-Export.tar.gz --force
```

For the official documentation click [here](https://docs.strapi.io/developer-docs/latest/developer-resources/data-management.html).
