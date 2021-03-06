---
title: Update Users Using Your Database
description: How to update user profiles when using your own database as an identity provider.
toc: true
topics:
    - updating-users
    - user-management
    - users
    - custom-database
contentType:
  - concept
  - how-to
useCase:
  - manage-users
---

# Update Users Using Your Database

You can update user profiles when using [your own database as an identity provider](/connections/database/custom-db) by:

* Using the [Management API](/api/management/v2#!/Users/patch_users_by_id).
* Updating the user in your database.
* [Enabling user migration](/users/migrations/automatic) from your database to Auth0.

## Update users with the Management API

When using your own database for authentication, you can use the [Management API](/api/management/v2) to update the following fields:

* `app_metadata`
* `user_metadata`
* `blocked`

If you need to update other user fields you will need to do it directly in your database.

## Update users in your database

You can update user profiles in your database as you normally do, and Auth0 will update its cached user profile the next time that user logs in.

See the [User profile cache](#user-profile-cache) section below for a brief overview of how Auth0 caches user profiles.

## Update users through migration

If you have [enabled user migration](/connections/database/migrating), and a user has already been migrated to the Auth0 database, then Auth0 will not query your database again for the user profile. And therefore all changes made in the custom database for that user will never reflect in Auth0.

Once a user has been migrated, you will also be able to update fields such as `email` and `email_verified` via the Management API. However, normal rules for updating other user fields will still apply as described in the [Normalized User Profile](/user-profile/normalized) (for example, you will still not be able to update fields such as `nickname`, `picture` and so on).

## User profile cache

Auth0 [caches the user profile](/user-profile/user-profile-details#caching-of-the-user-profile-in-auth0) received from a [database connection](/connections/database) before sending it to the client application. This cache is stored in the Auth0 database and is refreshed each time the user authenticates.

The cached values for the [Normalized User Profile](/user-profile/normalized) fields are based on the values returned from the Login Script of your custom database connection.
