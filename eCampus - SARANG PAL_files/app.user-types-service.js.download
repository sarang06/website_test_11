angular.module('ecampus.services').service('UserTypes', ['Storage', 'Service', function (Storage, Service) {
    if (!Storage.has('user_types')) {
        Service.getUserTypes().then(function (res) {
            Storage.set('user_types', res.data);
        }, function (res) {
            console.log(res);
        })
    }else{
        console.log('Available');
    }
}]);
