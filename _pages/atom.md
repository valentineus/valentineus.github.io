---
layout:    null
permalink: "/atom.xml"
sidebar:   false
---

<?xml version="1.0" encoding="utf-8"?>

<feed xmlns="http://www.w3.org/2005/Atom">
    <!-- Identifiers and references -->
    <link href="{{ site.rss | absolute_url | xml_escape }}" rel="self" type="application/atom+xml" />
    <link href="{{ site.url | xml_escape }}" rel="alternate" type="text/html" />
    <id>{{ site.url | xml_escape }}</id>

    <!-- Description and name -->
    <icon>{{ "/assets/favicon-32x32.png" | absolute_url | xml_escape }}</icon>
    <title>{{ site.title | smartify | strip_html | normalize_whitespace | xml_escape }}</title>
    <subtitle>{{ site.description | smartify | strip_html | normalize_whitespace | xml_escape }}</subtitle>
    <updated>{{ site.time | date_to_xmlschema }}</updated>

    <!-- Author -->
    <author>
        <email>{{ site.author.email | xml_escape }}</email>
        <name>{{ site.author.name | xml_escape }}</name>
        <uri>{{ site.author.url | xml_escape }}</uri>
    </author>

    {% for node in site.posts %}
        <!-- Full size record -->
        <entry>
            <!-- Identifiers and references -->
            <link href="{{ node.url | absolute_url | xml_escape }}" rel="alternate" type="text/html" />
            <id>{{ node.url | absolute_url | xml_escape }}</id>

            <!-- Description and name -->
            <title>{{ node.title | smartify | strip_html | normalize_whitespace | xml_escape }}</title>
            <summary>{{ node.description | smartify | strip_html | normalize_whitespace | xml_escape }}</summary>
            <updated>{{ node.latest_update | default: node.date | date_to_xmlschema }}</updated>
            <published>{{ node.date | date_to_xmlschema }}</published>

            <!-- Author -->
            <author>
                <email>{{ site.author.email | xml_escape }}</email>
                <name>{{ site.author.name | xml_escape }}</name>
                <uri>{{ site.author.url | xml_escape }}</uri>
            </author>

            <!-- Content -->
            <content type="html" xml:base="{{ node.url | absolute_url | xml_escape }}">
                {{ node.content | strip | strip_newlines | xml_escape }}
            </content>
        </entry>
    {% endfor %}
</feed>