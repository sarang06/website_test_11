angular.module('ecampus').controller('LoginController', ['$scope', '$rootScope', 'Service', 'Storage', '$state', function ($scope, $rootScope, Service, Storage, $state) {

    /* function to log in */
    $scope.loginData = {};
    $scope.doLogin = function () {
        if ($scope.loginData.disabled) {
            return false;
        }
        if (!($scope.loginData.username) || !($scope.loginData.password) || $scope.loginData.username.trim() === "" || $scope.loginData.password.trim() === "") {
            return false;
        }
        $scope.loginData.disabled = true;
        Service.login($scope.loginData).then(function (res) {
            $scope.loginData.disabled = false;
            $rootScope.userType = res.data.type;
            var ecampus_auth = {
                'token': res.data.auth_token,
                'type': res.data.type,
                'id': res.data.id,
                'status': res.data.status,
                'fullname': res.data.full_name,
                'username': res.data.username
            };
            Storage.set('ecampus_auth', ecampus_auth);
            $rootScope.$broadcast('userLoggedIn');
            $state.go('index.home');
        }, function (res) {
            $scope.loginData.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.forgetPasswordPopup = function () {
        swal({
            title: 'Forget Password ?',
            type: 'question',
            input: 'text',
            showCancelButton: true,
            confirmButtonText: 'Submit',
            showLoaderOnConfirm: true,
            inputPlaceholder: "Enter Your Email Address"
        }).then(function (forgetEmail) {
            $scope.applyForForgetPassword(forgetEmail);
        })
    };

    $scope.forgetPasswordApplyObj = {};
    $scope.applyForForgetPassword = function (forgetEmail) {
        if ($scope.forgetPasswordApplyObj.disabled) {
            return false;
        }
        $scope.forgetPasswordApplyObj.disabled = true;
        Service.applyForForgetPassword($scope.forgetPasswordApplyObj).then(function (res) {
            $('#forgetPasswordModal').modal('hide');
            $scope.forgetPasswordApplyObj.disabled = false;
            $scope.forgetPasswordApplyObj.email = "";
            swal('Success', res.data.response, 'success').then(function (res) {
            });
        }, function (res) {
            $scope.forgetPasswordApplyObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.forgetPasswordData = {};
    $scope.forgetPasswordSubmit = function () {
        if ($scope.forgetPasswordData.confirmPassword != $scope.forgetPasswordData.password) {
            swal('Error', 'Password and confirm password should be same !', 'error');
        }
        else {
            if ($scope.forgetPasswordData.disabled) {
                return false;
            }
            $scope.forgetPasswordData.disabled = true;
            $scope.forgetPasswordData.token = $state.params.token;
            Service.forgetPasswordSubmit($scope.forgetPasswordData).then(function (res) {
                $scope.forgetPasswordData.disabled = false;
                swal('Success', res.data.response, 'success').then(function (res) {
                    $state.go('index.home');
                });
            }, function (res) {
                $scope.forgetPasswordData.disabled = false;
                swal('Error', res.data.message, 'error');
            });
        }
    };

    $scope.resetAdminPasswordObj = {};
    $scope.resetAdminPassword = function () {
        if ($scope.resetAdminPasswordObj.confirmPassword != $scope.resetAdminPasswordObj.password) {
            swal('Error', 'Password and confirm password should be same !', 'error');
        }
        else {
            if ($scope.resetAdminPasswordObj.disabled) {
                return false;
            }
            $scope.resetAdminPasswordObj.disabled = true;
            Service.resetAdminPassword($scope.resetAdminPasswordObj).then(function (res) {
                $scope.resetAdminPasswordObj.disabled = false;
                swal('Success', res.data.response, 'success').then(function (res) {
                    $state.reload();
                });
            }, function (res) {
                $scope.resetAdminPasswordObj.disabled = false;
                swal('Error', res.data.message, 'error');
            });
        }
    };

    $scope.yourEnrollObj = {};
    $scope.getYourEnrollmentSubmit = function () {
        if ($scope.yourEnrollObj.disabled) {
            return false;
        }
        $scope.yourEnrollObj.disabled = true;
        Service.getYourEnrollment($scope.yourEnrollObj).then(function (res) {
            $scope.yourEnrollObj.disabled = false;
            $scope.newEnrollment = res.data.response;
        }, function (res) {
            $scope.yourEnrollObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

}]);