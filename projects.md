---
layout: page
title: Retired Projects
has_toc: false
nav_order: 40
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

<h1>Retired Projects</h1>
***

{: .fs-5}
This page lists all the **Projects** in The Apache Attic, see also the
[Retired Sub-Projects page]({% link subprojects.md %}).


{% assign project_array = site.data.project_array |  where: "project_type", "PMC" -%}

|Project|Type|Description|Retired|
|:------|:---|:----------|:------|
{%- for project in project_array %}
|{{forloop.index}}. [{{project.project_apachename}}](
   {%- link {{project.project_id | prepend: "projects/" | append: ".html"}} -%}
)|{{project.project_type}}|{{project.project_shortdesc}}|{{project.retirement_date | date: "%b %Y"}}
{%- endfor %}


