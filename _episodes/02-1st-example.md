---
title: "First Example"
teaching: 5
exercises: 0
questions:
- "How do I wrap a simple command line tool?"
objectives:
- "Learn the basic structure of a CWL description."
keypoints:
- "CWL documents are written in YAML and/or JSON."
- "The command called is specified with `baseCommand`."
- "Each expected input is described in the `inputs` section."
- "Input values are specified in a separate YAML file."
- "The tool description and input files are provided as arguments to a CWL runner."
---
The simplest "hello world" program.  This accepts one input parameter, writes a message to the terminal or job log, and produces
no permanent output. CWL documents are written in [JSON][json] or [YAML][yaml], or a mix of the two.

First, create a file called `1st-tool.cwl`, containing the boxed text below. It will help you to use a text editor that can be
specified to produce text in YAML or JSON. Whatever text editor you use, the indents you see should not be created using tabs.

*1st-tool.cwl*
~~~
{% include cwl/02-1st-example/1st-tool.cwl %}
~~~
{: .source}

Next, create a file called `echo-job.yml`, containing the following boxed text, which will describe the input of a run:

*echo-job.yml*
~~~
{% include cwl/02-1st-example/echo-job.yml %}
~~~
{: .source}

Now, invoke `cwl-runner` with the tool wrapper `1st-tool.cwl` and the input object echo-job.yml on the command line. The command
is  `cwl-runner 1st-tool.cwl echo-job.yml`. The boxed text below shows this command and the expected output.

~~~
$ cwl-runner 1st-tool.cwl echo-job.yml
[job 1st-tool.cwl] /tmp/tmpmM5S_1$ echo \
    'Hello world!'
Hello world!
[job 1st-tool.cwl] completed success
{}
Final process status is success

~~~
{: .output}

The command `cwl-runner 1st-tool.cwl echo-job.yml` is an example of a general form that you will often come across while using
CWL. The general form is `cwl-runner [tool-or-workflow-description] [input-job-settings]`

What's going on here?  Let's break down the contents of `1st-tool.cwl`:

~~~
cwlVersion: v1.0
class: CommandLineTool
~~~
{: .source}

The `cwlVersion` field indicates the version of the CWL spec used by the document.  The `class` field indicates this document
describes a command line tool.

~~~
baseCommand: echo
~~~
{: .source}

The `baseCommand` provides the name of program that will actually run (`echo`). `echo` is a built-in program in the bash and
C shells.

~~~
inputs:
  message:
    type: string
    inputBinding:
      position: 1
~~~
{: .source}

The `inputs` section describes the inputs of the tool.  This is a list of input parameters and each parameter includes an
identifier, a data type, and optionally an `inputBinding` which describes how this input parameter should appear on the command
line.  In this example, the `position` field indicates where it should appear on the command line.

~~~
outputs: []
~~~
{: .source}

This tool has no formal output, so the `outputs` section is an empty list.

[json]: http://json.org
[yaml]: http://yaml.org
[echo]: http://www.linfo.org/echo.html

{% include links.md %}
