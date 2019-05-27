angular.module('ecampus.services').factory('AuthTokenInterceptor', ['$q', 'Storage', '$location', function ($q, Storage, $location) {
    return {
        request: function (config) {
            var authToken = '';
            if (Storage.has("ecampus_auth")) {
                authToken = Storage.get("ecampus_auth", true).token;
            }
            config.headers = config.headers || {};
            if (authToken) {
                config.headers.Authorization = 'Bearer ' + authToken;
            }
            return config || $q.when(config);
        },
        responseError: function (rejection) {
            var errorArray = [];
            if (rejection.status == 422) {
                angular.forEach(rejection.data, function (val) {
                    errorArray.push(val[0]);
                    console.log(errorArray);
                });
                rejection.data.message = errorArray.join(' ');
            }
            if (rejection.status == 401 && rejection.data.error == 'unauthenticated') {
                if (Storage.has("ecampus_auth")) {
                    Storage.clear('ecampus_auth');
                    $location.path('/login')
                }
            }
            return $q.reject(rejection);
        }
    };
}]);
