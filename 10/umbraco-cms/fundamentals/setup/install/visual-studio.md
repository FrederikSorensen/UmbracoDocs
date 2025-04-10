---
description: A guide to install Umbraco CMS using Visual Studio.
---

# Install using Visual Studio

## Prerequisites

* Install the newest [Umbraco dotnet templates](install-umbraco-with-templates.md).
  * In Visual Studio 2022, the .NET CLI templates are enabled to appear, by default. For information on how to enable .NET CLI templates in Visual Studio 2019, see the [.NET CLI Templates in Visual Studio](https://devblogs.microsoft.com/dotnet/net-cli-templates-in-visual-studio/) article.
* Check the [Requirements](../requirements.md) to ensure you have everything you need to start your Umbraco project.

## Quick start

This is an abbreviated version of the installation steps. Jump to the [Create a new project](visual-studio.md#new-project) section for a more thorough guide.

* Open Visual Studio.
* Go to `File` > `New` > `Project`, search for **Umbraco**.
* Choose **Umbraco Project (Umbraco HQ)** then click **Next**.
* Choose or specify the parameters, leave the default or leave them all empty.
* Click **Create**.
* Use **CTRL+F5** to run the project and start the Umbraco installer.

## Video Tutorial

{% embed url="https://www.youtube.com/watch?ab_channel=UmbracoLearningBase&v=CDeAYGu_-cI" %}
How to install Umbraco using NuGet and Visual Studio
{% endembed %}

## Create a new Umbraco project

To install Umbraco we first need to install Umbraco's dotnet new templates.

For more information check the first 2 steps of the [Install Umbraco with .NET CLI article](install-umbraco-with-templates.md#install-the-template).

### Create the Visual Studio project

Go to **File > New > Project** and search for `Umbraco` in the _Search for templates_ field.

![The Create a new project dialog in Visual Studio.](images/VS/create-project.png)

Once you select **Umbraco Project (Umbraco HQ)** navigate to the next step by selecting _Next_.

### Configure the project

In this step, you will be able to give your project a name specific to the project you are creating.

![The Configure your new project dialog in Visual Studio.](images/VS/configure-project.png)

{% hint style="info" %}
Refrain from changing the Solution name, as this will cause a namespace conflict with the CMS itself.
{% endhint %}

### Adding additional information

In the next step, you are able to specify some additional parameters like the _Target framework_. The rest are optional.

![The Additional information dialog in Visual Studio.](images/VS/Umbraco10\_install.png)

You can then click the _Create_ button and your Umbraco Project will be ready for you.

![Overview of files in the project solution](images/VS/ready-solution.png)

### Running the site

You can now run the site through Visual Studio using **F5** or the **Debug** button.

Follow the installation wizard and after a few steps, you will get a message saying the installation was a success.

## Next steps

You are now ready to start building your Umbraco project. Have a look below for different resources on the next steps.

* [Getting Started with Umbraco](../../../../getting-started/)
* [Tutorial: Create a website from scratch](../../../tutorials/creating-a-basic-website/)
* [Find different options for hosting your Umbraco website](../server-setup/)
* [Learn about configuration in Umbraco CMS](../../../reference/configuration/)
