# Create Your First Generated Connector in Ballerina

## Introduction

Ballerina is a language designed for seamless integration, offering an extensive pre-built library ecosystem. Connectors in Ballerina are specialized packages that simplify communication with external services, typically through REST APIs. They eliminate the complexity of handling API interactions, allowing developers to effortlessly integrate third-party services into their Ballerina applications.

In addition to its rich library ecosystem, Ballerina makes it easy for developers to create, publish, and maintain custom connectors (client SDKs). These connectors can be shared on Ballerina Central, enabling the entire developer community to benefit from reusable integrations.

In this guide, we’ll show you how to generate your first Ballerina connector using OpenAPI specifications. This approach is one of the fastest and most efficient ways to build connectors, enabling you to quickly integrate external services into your Ballerina projects.

## Prerequisites

Before we begin, make sure you have:

1. Basic knowledge of Ballerina and Ballerina [installed](https://ballerina.io/downloads/) on your system (the latest version recommended).
2. GitHub account.
3. Git installed on your local machine.
4. Visual Studio Code with the Ballerina extension installed.

## Step 1: Setting Up the GitHub Repository

1. Go to GitHub and create a new repository. Name it following the pattern: `module-ballerinax-<connector-name>`. For example, `module-ballerinax-myconnector`. 

> More information on Ballerina connector naming conventions can be found in the [Ballerina connector development guide](https://github.com/ballerina-platform/ballerina-library/blob/main/docs/connector-development-process.md#naming-convention).

2. Clone your newly created empty repository to your local machine:
   ```
   git clone https://github.com/your-username/module-ballerinax-myconnector.git
   cd module-ballerinax-myconnector
   ```

3. Visit the [Ballerina generated connector template](https://github.com/ballerina-platform/ballerina-library/tree/main/library-templates/generated-connector-template) on GitHub.

4. Download or copy the contents from [Ballerina generated connector template](https://github.com/ballerina-platform/ballerina-library/tree/main/library-templates/generated-connector-template) on GitHub to your local repository folder. Make sure to include all files and directories.

5. Your local project structure should now look similar to this:
   ```
   module-ballerinax-myconnector/
   ├── .github/
   │   └── workflows/
   │       ├── CODEOWNERS
   │       └── pull_request_template.md
   ├── ballerina/
   │   ├── Ballerina.toml
   │   ├── Module.md
   │   ├── Package.md
   │   ├── build.gradle
   │   └── client.bal
   ├── build-config/
   │   └── resources/
   │       └── Ballerina.toml
   ├── docs/
   │   └── spec/
   │       └── sanitations.md
   ├── examples/
   │   ├── README.md
   │   ├── build.gradle
   │   └── build.sh
   ├── gradle/
   │   └── wrapper/
   │       ├── gradle-wrapper.jar
   │       └── gradle-wrapper.properties
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

## Step 3: Defining the OpenAPI Specification

1. Create a new file named `api_spec.yaml` in the `myconnector` directory.

2. Define a simple OpenAPI specification for your hypothetical API. Here's a generic example:

## Step 4: Generating the Connector

Ballerina provides a tool to generate connector code from OpenAPI specifications. Let's use it to create our connector:

1. Run the following command in your terminal:
   ```
   bal openapi -i myconnector/api_spec.yaml --mode client -o myconnector
   ```

2. This will generate the connector code in your `myconnector` directory.

## Step 5: Writing Examples

Let's create some example usage of our new connector:

1. Create a new file named `examples.bal` in the `myconnector/examples` directory.

2. Add the following content:

   ```ballerina
   import ballerina/io;
   import ballerinax/myconnector;
   
   public function main() returns error? {
       myconnector:Client myClient = check new("https://api.example.com/v1");
   
       // List resources
       var resources = check myClient->listResources();
       io:println("All resources: ", resources);
   
       // Get a specific resource
       var resource = check myClient->getResourceById("resource123");
       io:println("Resource with ID 'resource123': ", resource);
   }
   ```

## Step 6: Updating Documentation

1. Update the `Package.md` file in the `myconnector` directory with a brief description of your connector and its usage.

2. Update the main `README.md` file in the root directory with more detailed information about the connector, its features, and how to use it.

## Step 7: Committing and Pushing Changes

1. Stage your changes:
   ```
   git add .
   ```

2. Commit your changes:
   ```
   git commit -m "Initial connector implementation"
   ```

3. Push your changes to GitHub:
   ```
   git push origin main
   ```

## Step 8: Setting Up CI/CD (Optional)

The template includes GitHub Actions workflows for CI/CD. You may need to adjust these according to your specific needs.

## Conclusion

Congratulations! You've created your first generated Ballerina connector using the OpenAPI tool. This approach allows for rapid development of connectors that accurately reflect the underlying API structure.

Remember to keep your connector up-to-date with any changes in the OpenAPI specification and to test thoroughly, especially after making custom modifications.

For more detailed information on connector development and the OpenAPI tool, please refer to the [official Ballerina documentation](https://ballerina.io/learn/openapi-tool/).
