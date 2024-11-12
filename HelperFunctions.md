# Helper Class Documentation

The `Helper` class provides utility functions for the FluentCommunity plugin. This documentation is intended for developers working with the plugin.

## Methods

### getPortalSlug()

Retrieves the portal slug.

**Returns:** string
- The portal slug.

**Description:**
This method returns the portal slug, which can be filtered using the `fluent_community/portal_slug` hook.

---

### getPortalRouteType()

Gets the portal route type.

**Returns:** string
- The portal route type.

**Description:**
Returns the portal route type, defaulting to 'WebHistory'. Can be filtered using the `fluent_community/portal_route_type` hook.

---

### isHeadless()

Checks if the portal is in headless mode.

**Returns:** bool
- True if headless, false otherwise.

**Description:**
Determines if the portal is running in headless mode. Can be filtered using the `fluent_community/portal_page_headless` hook.

---

### hasColorScheme()

Checks for color scheme support.

**Returns:** bool
- True if color scheme is supported, false otherwise.

**Description:**
Checks if the portal has a color scheme. Can be filtered using the `fluent_community/has_color_scheme` hook.

---

### isSiteAdmin($userId = null)

Checks if a user is a site admin.

**Parameters:**
- `$userId` (int|null): The user ID to check. If null, checks the current user.

**Returns:** bool
- True if the user is a site admin, false otherwise.

**Description:**
Determines if the specified user (or current user if not specified) has site admin capabilities.

---

### baseUrl($path = '')

Generates the base URL for the portal.

**Parameters:**
- `$path` (string): The path to append to the base URL.

**Returns:** string
- The full base URL.

**Description:**
Generates the base URL for the portal, optionally appending a specified path.

---

### getCurrentProfile($cached = true)

Retrieves the current user's profile.

**Parameters:**
- `$cached` (bool): Whether to use cached profile data.

**Returns:** XProfile|null
- The user's profile object or null if not found.

**Description:**
Retrieves the current user's profile. Returns an `XProfile` object if found, or null otherwise.

---

### getCurrentUser($cached = true)

Gets the current user model.

**Parameters:**
- `$cached` (bool): Whether to use cached user data.

**Returns:** User|false
- The User model or false if not found.

**Description:**
Retrieves the current user. Returns a `User` object if found, or false otherwise.

---

### getMenuItemsGroup($context = 'view')

Retrieves the menu items group.

**Parameters:**
- `$context` (string): The context for getting menu items.

**Returns:** array
- The menu items group.

**Description:**
Retrieves the menu items group based on the given context. The context can be 'view' or 'edit'.

---

### getMediaFromUrl($url)

Retrieves a media object from a URL.

**Parameters:**
- `$url` (string|array): The URL or an array containing URL information.

**Returns:** Media|null
- The Media object if found, null otherwise.

**Description:**
Attempts to retrieve a Media object based on the provided URL or URL information.

---

### encryptDecrypt($value, $type = 'e')

Encrypts or decrypts a value.

**Parameters:**
- `$value` (string): The value to encrypt or decrypt.
- `$type` (string): The type of operation ('e' for encrypt, 'd' for decrypt).

**Returns:** string|false
- The encrypted or decrypted value, or false if an error occurs.

**Description:**
Encrypts or decrypts a value using OpenSSL. The method uses AES-256-CTR encryption.

---

### getIp($anonymize = false)

Gets the user's IP address.

**Parameters:**
- `$anonymize` (bool): Whether to anonymize the IP address.

**Returns:** string
- The IP address.

**Description:**
Retrieves the user's IP address, with an option to anonymize it. It handles various server configurations and proxies.

This documentation covers some of the key methods in the `Helper` class. Each method is presented with its signature, parameters, return type, and a brief description of its functionality. This format should be more suitable for developers working with the FluentCommunity plugin.


### addUserToSpace($spaceId, $userId, $role, $by)

Adds a user to a space.

**Parameters:**
- `$spaceId` (int): The ID of the space.
- `$userId` (int): The ID of the user.
- `$role` (string): The role of the user in the space.
- `$by` (string): The method of adding the user to the space.

**Returns:** bool
- True if added, false if the member is already in the space or no user or space found in the system.

### removeFromSpace($spaceId, $userId, $by)

Removes a user from a space.

**Parameters:**
- `$spaceId` (int): The ID of the space.
- `$userId` (int): The ID of the user.
- `$by` (string): The method of removing the user from the space. 'by_admin' or 'self'.

**Returns:** bool
- True if removed, false if the member is not in the space or no user or space found in the system.
