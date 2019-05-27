angular.module('ecampus.services').factory('Storage', ['$cookies', function ($cookies) {
    return {
        get: function (key, toJson) {
            var value = $cookies.get(key);
            return toJson ? angular.fromJson(value) : value;
        },
        set: function (key, value) {
            var val = typeof value === "object" ? angular.toJson(value) : value;
            $cookies.put(key, val);
        },
        has: function (key) {
            return $cookies.get(key) !== undefined;
        },
        clear: function (keys) {
            var keysToClear = keys.split(" ");
            angular.forEach(keysToClear, function (key) {
                $cookies.remove(key);
            });
        }
    };
}]);