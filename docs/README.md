# Create Your First Ballerina Connector

## Introduction

Ballerina is a programming language designed for smooth integration, offering a large library of pre-built connectors. These connectors are special packages that make it easy to communicate with external services, usually through REST APIs. By using connectors, developers can quickly integrate third-party services into their Ballerina applications without having to worry about the technical details of API interactions.

Along with its powerful library ecosystem, Ballerina also allows developers to easily create, share, and manage their own custom connectors. These connectors can be published on Ballerina Central, making them available for the entire community to use and reuse in their projects.

In this guide, we'll walk you through how to generate your first Ballerina connector using an OpenAPI specification. This is one of the fastest and easiest ways to build connectors, helping you quickly integrate external services into your Ballerina projects.

## Prerequisites

Before we begin, make sure you have:

1. A basic understanding of Ballerina SwanLake and the [latest version installed](https://ballerina.io/downloads/).
2. An OpenAPI specification of the API for which you’re building the connector, along with API credentials (e.g., Twitter Developer account).
3. A GitHub account, and Git installed locally.
4. Visual Studio Code with the [Ballerina extension](https://marketplace.visualstudio.com/items?itemName=WSO2.ballerina).

## Step 1: Setting up the project structure

1. Create a new GitHub repository with an appropriate name. For Ballerina official connectors, the repository name will follow the pattern: `module-ballerinax-<connector-name>` (e.g., `module-ballerinax-twitter`). But for custom connectors, you can choose a name that suits your connector.

2. Clone your newly created empty repository to your local machine:
   ```bash
   git clone https://github.com/<your-username>/<connector-repo-name>.git
   cd <connector-repo-name>
   ```

3. Visit the [Ballerina generated connector template on GitHub](https://github.com/ballerina-platform/ballerina-library/tree/main/library-templates/generated-connector-template/files) and copy the entire project structure and content to your local repository folder, making sure to include all files and directories.

4. Your local project structure should now look similar to this:
   ```
   module-ballerinax-myconnector/
   ├── .github/
   ├── ballerina/
   │   ├── Ballerina.toml
   │   ├── Module.md
   │   ├── Package.md
   │   ├── build.gradle
   │   └── client.bal
   ├── build-config/
   ├── docs/
   │   └── spec/
   │       └── sanitations.md
   ├── examples/
   │   ├── README.md
   │   ├── build.gradle
   │   └── build.sh
   ├── gradle/
   ├── .gitignore
   ├── LICENSE
   ├── README.md
   ├── build.gradle
   ├── gradle.properties
   ├── gradlew
   ├── gradlew.bat
   └── settings.gradle
   ```

> **Tip**: The template includes placeholders for various fields. To update them with your connector-specific metadata, use the provided [Ballerina script](https://github.com/ballerina-platform/ballerina-library/blob/main/library-templates/generated-connector-template/scripts/replace_placeholders.bal).

Detailed information on the Ballerina connector structure can be found in the [Ballerina module contribution guide](https://github.com/ballerina-platform/ballerina-library/blob/main/docs/adding-a-new-ballerina-module.md#directory-structure).

## Step 2: Preparing the OpenAPI Specification

1. Find the OpenAPI specification for the API you want to create a connector for. This is usually available in the API documentation.
   Example: For Twitter, you can get the latest API specification from the [Twitter OpenAPI endpoint](https://api.twitter.com/2/openapi.json).

2. Save the file as `spec.yaml` (or `spec.json`) in the `docs/spec` directory of your project.

3. You may need to sanitize the OpenAPI specification to ensure compatibility with the Ballerina OpenAPI tool. This process may involve:
   - Renaming schema names to comply with Ballerina naming conventions.
   - Adding, removing, or modifying security schemes to customize authentication options.

## Step 3: Generating the connector

With your OpenAPI spec ready, use the [Ballerina OpenAPI tool](https://ballerina.io/learn/openapi-tool/) to generate the connector code.

1. In your terminal, run the following command from the project root:
   ```bash
   bal openapi -i path/to/spec --mode client -o ballerina
   ```

   Example for Twitter:
   ```bash
   bal openapi -i docs/spec/openapi.json --mode client -o ballerina
   ```

   This will generate the connector code in your `ballerina` directory.

2. Make sure that the generated client consists of the following files:
   - `client.bal`: Contains the client implementation with all the API operations.
   - `types.bal`: Contains the data types used in the client.
   - `utils.bal`: Contains utility functions used in the client.

## Step 4: Testing the connector

Now that your connector is generated, it’s important to write tests to ensure everything works as expected.

1. In the `ballerina/tests` directory, add the required test files and write test cases for the key operations of your connector. Aim to cover as many API use cases as possible.

2. Execute the tests using the `bal test` command to verify the functionality of your connector.

> For detailed guidance on writing tests, check the [Ballerina testing guide](https://ballerina.io/learn/test-ballerina-code/test-a-simple-function/).

> For sample implementations, refer to the [test implementation of the Ballerina Twitter connector](https://github.com/ballerina-platform/module-ballerinax-twitter/tree/main/ballerina/tests).

## Step 5: Documenting the connector

Documentation is crucial for helping others understand and use your connector effectively.

1. **Update `Module.md` and `Package.md`**: In the `ballerina` directory, update these files with:
   - **Overview**: A brief introduction to the connector.
   - **Setup**: How to configure and start using the connector.
   - **Quickstart**: A simple example to get users started.
   - **Examples**: Detailed code samples.

2. **Update `README.md`**: Update the main `README.md` file in the project root to provide comprehensive information about your connector, including its features and usage.

3. **Add Examples**: Place real-world usage examples in the `examples/` directory.

## Step 6: Publishing the connector

Once you’ve completed the development and testing of your connector, it’s time to publish it for others to use.

1. Make sure to update the `Ballerina.toml` file with the following details:
   - `org`: Your organization name.
   - `name`: The name of your connector.
   - `version`: The version of your connector.
   - `license`: The license under which your connector is distributed.
   - `authors`: Your name and email address.
   - `keywords`: Keywords to help users find your connector.
   - `icon`: The relative path to the icon file.
   - `repository`: The URL of your GitHub repository.

2. Follow the steps in the [Ballerina package publishing guide](https://ballerina.io/learn/publish-packages-to-ballerina-central/) to publish your connector to Ballerina Central under your organization.

---

Congratulations! You've successfully created your first Ballerina connector using OpenAPI. This process allows you to quickly integrate external services and share your connector with the Ballerina community.

Remember to keep your connector up to date with any changes in the API’s OpenAPI specification and to test thoroughly whenever updates are made.

Also, ensure you comply with the API’s terms of service when developing and distributing your connector.
