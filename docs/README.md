# Create Your First Generated Connector in Ballerina

## Introduction

Ballerina is a language designed for seamless integration, offering an extensive pre-built library ecosystem. Connectors in Ballerina are specialized packages that simplify communication with external services, typically through REST APIs. They eliminate the complexity of handling API interactions, allowing developers to effortlessly integrate third-party services into their Ballerina applications.

In addition to its rich library ecosystem, Ballerina makes it easy for developers to create, publish, and maintain custom connectors (client SDKs). These connectors can be shared on Ballerina Central, enabling the entire developer community to benefit from reusable integrations.

In this guide, we’ll show you how to generate your first Ballerina connector using OpenAPI specifications. This approach is one of the fastest and most efficient ways to build connectors, enabling you to quickly integrate external services into your Ballerina projects.

## Prerequisites

Before we begin, make sure you have:

1. Basic knowledge of Ballerina and Ballerina [installed](https://ballerina.io/downloads/) on your system (the latest version recommended).
2. OpenAPI specification and API credentials of the service for which you're creating a connector for (e.g., Twitter Developer account and API credentials).
3. GitHub account and Git installed on your local machine.
4. Visual Studio Code editor with the [Ballerina extension](https://marketplace.visualstudio.com/items?itemName=WSO2.ballerina) installed.

## Step 1: Setting Up the GitHub Repository

1. Create a new GitHub repository with an appropriate name. For Ballerina official connectors, the repository name will follow the pattern: `module-ballerinax-<connector-name>` (e.g., `module-ballerinax-twitter`). But for custom connectors, you can choose a name that suits your connector.

2. Clone your newly created empty repository to your local machine:
   ```
   git clone https://github.com/<your-username>/<connector-repo-name>.git
   cd <connector-repo-name>
   ```

3. Visit the [Ballerina generated connector template](https://github.com/ballerina-platform/ballerina-library/tree/main/library-templates/generated-connector-template) on GitHub.

4. Download or copy the contents from [Ballerina generated connector template](https://github.com/ballerina-platform/ballerina-library/tree/main/library-templates/generated-connector-template) on GitHub to your local repository folder. Make sure to include all files and directories.

5. Your local project structure should now look similar to this:
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

> Note: More information on the structure of a Ballerina connector can be found in the [Ballerina module contribution guide](https://github.com/ballerina-platform/ballerina-library/blob/main/docs/adding-a-new-ballerina-module.md#directory-structure).

> Note: All the variables in the project template are added as placeholders. You can replace them with your own values by using [this Ballerina script](https://github.com/ballerina-platform/ballerina-library/blob/main/library-templates/generated-connector-template/scripts/replace_placeholders.bal).

## Step 2: Preparing the OpenAPI Specification

1. Find the OpenAPI specification for the API you want to create a connector for. This is usually available in the API documentation.
   Example: For Twitter, you can get the latest API specification from [Twitter OpenAPI endpoint](https://api.twitter.com/2/openapi.json).

2. Save this file as `spec.yaml`(or `spec.json`) under the `docs/spec` directory, and ensure that the OpenAPI specification is valid and complete. 

3. You may need to sanitize the OpenAPI specification to ensure compatibility with the Ballerina OpenAPI tool. This process may involve:
  - Renaming schema names to comply with Ballerina naming conventions.
  - Adding, removing, or modifying security schemes to customize authentication options.

## Step 3: Generating the Connector

Use Ballerina's OpenAPI tool to generate your connector:

1. Run the following command in your terminal on the root directory of your project:
   ```
   bal openapi -i path/to/spec --mode client -o ballerina
   ```

   Example for Twitter:
   ```
   bal openapi -i docs/spec/openapi.josn --mode client -o ballerina
   ```

   This will generate the connector code in your `ballerina` directory.

2. Make sure that the generated client will consist of the following files:
- `client.bal`: Contains the client implementation with all the API operations.
- `types.bal`: Contains the data types used in the client.
- `utils.bal`: Contains utility functions used in the client.

## Step 5: Testing the Connector

1. Navigate to the `ballerina/tests` directory and create a new Ballerina test file to test the connector operations.
2. Implement test cases for the most common use cases (or all use cases if possible) related to the connector operations.

> Note: More information on writing tests can be found in the [Ballerina testing guide](https://ballerina.io/learn/test-ballerina-code/test-a-simple-function/).

## Step 6: Updating Documentation

1. Update the `Module.md` and `Package.md` files in the `ballerina` directory with the sections below:
   - **Overview**: A brief description of the connector and its purpose. 
   - **Setup guide**: Instructions on how to set up and use the connector.
   - **Quickstart**: A simple example demonstrating how to use the connector.
   - **Examples**: links to example code demonstrating the connector's usage.
2. Update the main `README.md` file in the root directory with more detailed information about the connector, its features, and how to use it.
3. All the real world examples should be added to the `examples` directory.

## Conclusion

Congratulations! You've successfully completed your first Ballerina connector using the OpenAPI tool.

Remember to keep your connector up-to-date with any changes in the OpenAPI specification and to test thoroughly, especially after making custom modifications.

> Note: Always ensure you're complying with the API's terms of service and usage guidelines when developing and using your connector.
