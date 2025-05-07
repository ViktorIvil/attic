---
layout: page
title: Experimental
has_toc: false
nav_order: 50
---
{%- comment -%}
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements.  See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to you under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License.  You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
{% endcomment %}

# Experimental Page
***
This branch has a number of changes, for consideration:
 1. **Splitting** the Projects / Sub-Projects  into separate **lists** & **Navigation**(Sidebar)
   - [Retired Projects](projects.html)
   - [Retired Sub-Projects](subprojects.html)
 1. A [Project Index](projects-index.html) page
 1. This page showing [Mermaid Diagrams](https://just-the-docs.com/docs/ui-components/code/#mermaid-diagram-code-blocks):
   - [Attic Process Diagram](#attic-process-diagram)
   - [Project Retirements Graph](#project-retirements-graph)
   - [Project Retirements Timeline](#project-retirements-timeline)
   
## Attic Process Diagram

```mermaid
graph TD;
    accTitle: the Attic Process
    accDescr: Attic process diagram which shows the steps of moving a Retired Project to the Attic
    RESL("`1 **Confirm Board Resolution**`")
    JIRA("`**Create Attic JIRA**
        (to manage the move)`")
    PROJ("`2 **Create Project Page**
        on Attic Site`")
    USER("`3 **Inform Users**
        of move to Attic`")
    DOAP("`4 **Update Project DOAP**
        file (if any)`")
    LOCK("`5 **Lock Down Resources**
        (create Infra JIRA ticket)`")
    ANNC("`6 **Announce**
        *announce AT apache.org*`")
    RESL-->JIRA;
    RESL-->PROJ;
    JIRA<-->PROJ;
    PROJ-->USER;
    PROJ-->DOAP;
    PROJ-->LOCK;
    USER-->ANNC;
    DOAP-->ANNC;
    LOCK-->ANNC;
    click RESL "/process-howto.html#1-confirm-board-resolution"
    click PROJ "/process-howto.html#2-create-project-page-on-attic-site"
    click USER "/process-howto.html#3-inform-users-of-the-move-to-the-attic"
    click DOAP "/process-howto.html#4-update-the-project-doap-file-if-any"
    click LOCK "/process-howto.html#5-get-infra-to-lock-down-project-resources"
    click ANNC "/process-howto.html#6-announce-on-announce-at-apacheorg"
```

## Project Retirements Graph

The following graph shows the number of Projects retiring for each year (**NOT** including **Sub-Projects**).

{% assign sorted_years = site.data.years_array |  sort: 'year' -%}
{% assign no_of_years = 20 -%}
{% assign first = sorted_years | size | minus: no_of_years | at_least: 0 -%}
{% assign second = first | plus: 1 -%}
{% assign count_max = 0 -%}
{%- for year in sorted_years offset: first -%}
    {% assign count_max = count_max | at_least: year['p_count'] -%}
{%- endfor %}

{: .note}
This is currently configured to show the last **{{ no_of_years}} years** of retirements (easily changed through the `$no_of_years` variable).

```mermaid
xychart-beta
    title "Project Retirements by Year"
    x-axis "Year" [{{ sorted_years[first]['year']}}
     {%- for year in sorted_years offset: second -%}
       {{ year['year'] | prepend: ', '}}
     {%- endfor %}]
    y-axis "Number of Projects" 0 --> {{count_max | plus: 2 | at_least: 10}}
    bar [{{ sorted_years[first]['p_count']}}
     {%- for year in sorted_years offset: second -%}
       {{ year['p_count'] | prepend: ', '}}
     {%- endfor %}]
    line [{{ sorted_years[first]['p_count']}}
     {%- for year in sorted_years offset: second -%}
       {{ year['p_count'] | prepend: ', '}}
     {%- endfor %}]
```

## Project Retirements Timeline
The following timeline shows Projects retiring for each year (including Sub-Projects, if any).

{% assign no_of_years = 20 -%}
{% assign first = sorted_years | size | minus: no_of_years | at_least: 0 -%}

{: .note}
This is currently configured to show the last **{{ no_of_years}} years** of retirements (easily changed through the `$no_of_years` variable).

```mermaid
timeline
    title History of Project Retirements  
  {% for year in sorted_years offset: first %}
    {{ year['year'] }}
    {%- assign sorted_projects = year['projects']  | sort: 'retirement_date' -%}
    {%- for project in sorted_projects -%}
      {{ project['project_name'] | prepend: ' : '}}
    {%- endfor -%}
  {% endfor %}
```