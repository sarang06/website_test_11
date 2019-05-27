var socket = io('http://' + window.location.hostname + ':3000');

var ecampus = angular.module('ecampus', [
    'angular.filter',
    'angularMoment',
    'ecampus.services',
    'ng-bootstrap-select',
    'ngAnimate',
    'ngMaterial',
    'ngMessages',
    'ngJcrop',
    'oc.lazyLoad',
    'ui.bootstrap',
    'ui.router',
    'angucomplete-alt',
    'ngSanitize',
    'angular-nicescroll',
    'ui.tinymce',
    'daterangepicker',
    'moment-picker',
    'rzModule'
]);

ecampus.run(['$rootScope', '$state', 'Storage', function ($rootScope, $state, Storage) {
    $rootScope.$on('$stateChangeStart', function (evt, toState) {
        if (toState.authenticate && !Storage.has('ecampus_auth')) {
            evt.preventDefault();
            $state.go("login");
        }
        if (toState.onlyNonLogged && Storage.has('ecampus_auth')) {
            evt.preventDefault();
            $state.go('index.home')
        }
        if (Storage.get('ecampus_auth', true)) {
            $rootScope.userType = Storage.get('ecampus_auth', true).type;
            $rootScope.userStatus = Storage.get('ecampus_auth', true).status;
        }
        $rootScope.preloader = true;
    });
    $rootScope.$on('$stateChangeSuccess', function (evt, toState) {
        $rootScope.$broadcast('stateAuth', toState);
        if (toState.name == 'index.home') {
            evt.preventDefault();
            $state.go('index.home.news-feeds', {}, {
                location: false
            });
        }
        if (toState.name == 'index.attendance') {
            evt.preventDefault();
            $state.go('index.attendance.student-attendance', {}, {
                location: false
            });
        }
        if (toState.name == 'index.messages') {
            evt.preventDefault();
            $state.go('index.messages.inbox', {}, {
                location: false
            });
        }
        if (toState.name == 'index.appraisal') {
            evt.preventDefault();
            $state.go('index.appraisal.appraisal-form', {}, {
                location: false
            });
        }
        if (toState.name == 'index.time-table') {
            evt.preventDefault();
            $state.go('index.time-table.student-time-table', {}, {
                location: false
            });
        }
        if (toState.name == 'index.mentorship') {
            evt.preventDefault();
            $state.go('index.mentorship.amentor', {}, {
                location: false
            });
        }
        if (toState.name == 'index.feedback') {
            evt.preventDefault();
            $state.go('index.feedback.start-feedback', {}, {
                location: false
            });
        }
        if (toState.name == 'index.mentorship.edit-mentee-info') {
            evt.preventDefault();
            $state.go('index.mentorship.edit-mentee-info.personal-and-family-info', {}, {
                location: false
            });
        }
        if (toState.name == 'index.home.student-forms') {
            evt.preventDefault();
            $state.go('index.home.student-forms.personal-and-family-info', {}, {
                location: false
            });
        }
        if (toState.name == 'index.home.bus') {
            evt.preventDefault();
            $state.go('index.home.bus.manage-bus-route', {}, {
                location: false
            });
        }
        if (toState.name == 'index.mentorship.new-assign-mentor') {
            $rootScope.mentorId = $state.params.mentorid;
        }
        if (toState.name == 'index.mentorship.edit-mentee-info.semester-informations' || 'index.mentorship.edit-mentee-info.personal-and-family-info'
            || 'index.mentorship.edit-mentee-info.education-details' || 'index.mentorship.edit-mentee-info.training-and-placement-details') {
            $rootScope.studentId = $state.params.studentId;
        }
        $rootScope.currentState = $state.current.name;
        $rootScope.preloader = false;
    });
    $rootScope.$on('$viewContentLoaded', function () {
        $('.selectpicker').selectpicker();

    });
}]);

/*--Custom provider to set dynamic dashboard of all user--*/
ecampus.provider('userDetails', [function () {
    var $injector = angular.injector(['ecampus.services']);
    var localStorageObject = $injector.get('Storage');
    var user = {};
    this.returnUserFolder = function () {
        var user_types = [],
            folderName = '';
        user.isUser = !!localStorageObject.get('ecampus_auth');
        if (user.isUser) {
            user.type = localStorageObject.get('ecampus_auth', true).type;
            user_types = localStorageObject.get('user_types', true);
            angular.forEach(user_types, function (val, key) {
                if (val.id == user.type) {
                    folderName = val.folderName;
                }
            });
            return folderName;
        }
    };
    this.$get = function () {
        user.isUser = !!localStorageObject.get('ecampus_auth');
        if (user.isUser) {
            user.type = localStorageObject.get('ecampus_auth', true).type;
        }
        return user;
    };
}]);

/* --rules and states configuration for this application-- */
ecampus.config(['$stateProvider',
    '$urlRouterProvider',
    '$locationProvider',
    '$httpProvider',
    'userDetailsProvider',
    '$windowProvider',
    'ngJcropConfigProvider',
    function ($stateProvider,
              $urlRouterProvider,
              $locationProvider,
              $httpProvider,
              userDetailsProvider,
              $windowProvider,
              ngJcropConfigProvider) {
        var windowP = $windowProvider.$get();

        $urlRouterProvider.otherwise(function () {
            if (userDetailsProvider.$get().isUser) {
                return '/home';
            } else {
                return '/login';
            }
        });

        $urlRouterProvider.when('/home', ['$state', function ($state) {
            $state.go('index.home.news-feeds', {}, {
                location: true
            });
        }]);

        $urlRouterProvider.when('/home/training-placement', ['$state', function ($state) {
            $state.go('index.home.training-placement.news', {}, {
                location: true
            });
        }]);

        $urlRouterProvider.when('/mentorship/edit-mentee-info', ['$state', function ($state) {
            $state.go('index.mentorship.edit-mentee-info.personal-and-family-info', {}, {
                location: false
            });
        }]);

        $urlRouterProvider.when('/attendance', ['$state', function ($state) {
            $state.go('index.attendance.student-attendance', {}, {
                location: false
            });
        }]);

        $urlRouterProvider.when('/mentorship', ['$state', '$rootScope', function ($state, $rootScope) {
            if ($rootScope.userType == 15 || $rootScope.userType == 8) {
                $state.go('index.mentorship.assign-mentor', {}, {
                    location: false
                });
            } else {
                $state.go('index.mentorship.amentor', {}, {
                    location: false
                });
            }
        }]);

        $urlRouterProvider.when('/messages', ['$state', function ($state) {
            $state.go('index.messages.inbox', {}, {
                location: true
            });
        }]);

        $urlRouterProvider.when('/time-table', ['$state', function ($state) {
            $state.go('index.time-table.student-time-table', {}, {
                location: true
            });
        }]);

        $urlRouterProvider.when('/feedback', ['$state', function ($state) {
            $state.go('index.feedback.start-feedback', {}, {
                location: true
            });
        }]);

        /*rule to remove the slash in the last of url*/
        $urlRouterProvider.rule(function ($injector, $location) {
            var path = $location.path();
            var hasTrailingSlash = path[path.length - 1] === '/';
            if (hasTrailingSlash) {
                var newPath = path.substr(0, path.length - 1);
                return newPath;
            }
        });

        // Use the HTML5 History API
        $locationProvider.html5Mode({
            enabled: true
        });
        // [optional] To change the jcrop configuration
        ngJcropConfigProvider.setJcropConfig({
            bgColor: 'white',
            bgOpacity: 0.5,
            aspectRatio: 1
        });

        // Use the auth token interceptor to append the auth_token to every request
        $httpProvider.interceptors.push('AuthTokenInterceptor');

        $stateProvider
            .state('login', {
                url: '/login',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                controller: 'LoginController',
                templateUrl: 'views/login.html',
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ["angular/ng-controllers/app.loginController.js"]
                        });
                    }]
                },
                authenticate: false,
                onlyNonLogged: true
            })

            .state('forget-password', {
                url: '/forget-password/:token',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                controller: 'LoginController',
                templateUrl: 'views/forget-password.html',
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ["angular/ng-controllers/app.loginController.js"]
                        });
                    }]
                },
                authenticate: false,
                onlyNonLogged: true
            })
            .state('index', {
                url: '/',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/index.html';
                },
                authenticate: true,
                abstract: true
            })

            .state('index.home', {
                url: 'home',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/home.html';
                },
                authenticate: true
            })
            .state('index.home.news-feeds', {
                url: '/news-feeds',
                controller: 'NewsFeedController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/news-feed.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.NewsFeedController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.news-feeds-approve', {
                url: '/news-feeds-approve',
                controller: 'NewsFeedController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/newsfeeds/news-feeds-approve.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.NewsFeedController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.achievements', {
                url: '/achievements',
                controller: 'NewsFeedController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/achievements.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.NewsFeedController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.profile', {
                url: '/profile',
                controller: 'EditProfileController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/profile.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.editProfileController.js',
                                'angular/ng-controllers/app.NewsFeedController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.results', {
                url: '/results',
                controller: 'ResultController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/results.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.resultController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.results.mst-results', {
                url: '/mst-results',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/mst-results.html';
                },
                authenticate: true
            })
            .state('index.home.results.view-mst-results', {
                url: '/view-mst-result/:id/:mst',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-mst-result.html';
                },
                authenticate: true
            })
            .state('index.home.results.session-results', {
                url: '/session-results',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/sessional-results.html';
                },
                authenticate: true
            })
            .state('index.home.results.view-sessional-result', {
                url: '/view-sessional-result/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-sessional-result.html';
                },
                authenticate: true
            })
            .state('index.home.results.semester-results', {
                url: '/semester-results',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/semester-results.html';
                },
                authenticate: true
            })
            .state('index.home.results.view-semester-result', {
                url: '/view-semester-result/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-semester-result.html';
                },
                authenticate: true
            })
            .state('index.home.results.semester-grade-results', {
                url: '/semester-grade-results',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/semester-grades-results.html';
                },
                authenticate: true
            })
            .state('index.home.results.view-semester-grade-results', {
                url: '/view-semester-grade-results/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-semester-grade-result.html';
                },
                authenticate: true
            })
            .state('index.home.student-forms', {
                url: '/student-forms',
                controller: 'StudentFormController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/student-forms.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.studentFormController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.student-forms.personal-and-family-info', {
                url: '/personal-and-family-info',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/personal-and-family-info.html';
                },
                authenticate: true
            })
            .state('index.home.student-forms.training-and-placement-details', {
                url: '/training-and-placement-details',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/training-and-placement-details.html';
                },
                authenticate: true
            })
            .state('index.home.student-forms.education-details', {
                url: '/education-details',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/education-details.html';
                },
                authenticate: true
            })
            .state('index.home.student-forms.attendance-details', {
                url: '/attendance-details',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/attendance-details.html';
                },
                authenticate: true
            })
            .state('index.home.student-forms.semester-informations', {
                url: '/semester-informations',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/semester-information.html';
                },
                authenticate: true
            })
            .state('index.home.student-forms.achievements-and-awards', {
                url: '/achievements-and-awards',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/achievements-and-awards.html';
                },
                authenticate: true
            })
            .state('index.home.bus-route', {
                url: '/bus-route',
                controller: 'BusRouteController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/bus-route.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.busRouteController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.training-placement', {
                url: '/training-placement',
                controller: 'TandpController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/tandp.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.tandpController.js', 'angular/ng-controllers/app.NewsFeedController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.training-placement.news', {
                url: '/news',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/news.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.companies', {
                url: '/companies',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/companies.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.single-companies', {
                url: '/single-companies/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/single-companies.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.add-company', {
                url: '/add-company',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/add-company.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.consultancy', {
                url: '/consultancy',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/consultancy.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.single-consultancy', {
                url: '/single-consultancy/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/single-consultancy.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.add-consultancy', {
                url: '/add-consultancy',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/add-consultancy.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.add-placement-caricular', {
                url: '/add-placement-circular/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/add-placement-caricular.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.placement-circulars', {
                url: '/placement-circulars',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/placement-circulars.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.single-placement-circulars', {
                url: '/single-placement-circulars/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/single-placement-circulars.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.add-eligibility-criteria', {
                url: '/add-eligiblity-criteria/:circularId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/add-eligibility-criteria.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.eligiblity-criteria', {
                url: '/eligiblity-criteria',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/eligiblity-criteria.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.reports', {
                url: '/reports',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/reports.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.edit-single-consultancy', {
                url: '/edit-consultancy/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/edit-single-consultancy.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.edit-single-placement-circular', {
                url: '/edit-placement-circular/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/edit-single-placement-circular.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.edit-eligibility-criteria', {
                url: '/edit-eligibility-criteria/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/edit-eligibility-criteria.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.edit-single-company', {
                url: '/edit-company/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/edit-single-company.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.tnp-attendance', {
                url: '/tnp-attendance/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/tnp-attendance.html';
                },
                authenticate: true
            })
            .state('index.home.training-placement.eligible-students', {
                url: '/eligible-students/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/tandp/eligible-students.html';
                },
                authenticate: true
            })
            .state('index.home.chat', {
                url: '/chat',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/chat.html';
                },
                authenticate: true
            })
            .state('index.home.venue-booking', {
                url: '/venue-booking',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/venue-booking.html';
                },
                authenticate: true
            })
            .state('index.home.t-shirt', {
                url: '/t-shirt',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/t-shirt.html';
                },
                authenticate: true
            })
            .state('index.home.group-discussion', {
                url: '/group-discussion',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/group-discussion.html';
                },
                authenticate: true
            })
            .state('index.home.suggestion', {
                url: '/suggestion',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/suggestion.html';
                },
                authenticate: true
            })
            .state('index.home.post-grievance', {
                url: '/post-grievance',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                controller: 'GrievanceController',
                templateUrl: 'views/grievance/post-grievance.html',
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ["angular/ng-controllers/app.grievanceController.js"]
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.get-grievance', {
                url: '/grievance',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                controller: 'GrievanceController',
                templateUrl: 'views/grievance/grievance.html',
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ["angular/ng-controllers/app.grievanceController.js"]
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.suggestion-detail', {
                url: '/suggestion-detail/:suggetionId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/suggestion-detail.html';
                },
                authenticate: true
            })
            .state('index.home.accounts', {
                url: '/accounts',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/accounts.html';
                },
                authenticate: true
            })
            .state('index.home.view-accounts', {
                url: '/view-accounts',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/view-accounts.html';
                },
                authenticate: true
            })
            .state('index.home.teachers', {
                url: '/teachers',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/teachers.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js',
                                'angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.assign-subject-to-teachers', {
                url: '/assign-subject/:uid',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/assign-subject-to-teachers.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.other-staff-detail', {
                url: '/assign-subjects/:uid',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/assign-subject-to-other-teacher.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.all-faculties', {
                url: '/all-teachers',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/all-teacher.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.add-teacher', {
                url: '/add-teacher',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/add-teacher.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.hod', {
                url: '/hod',
                controller: 'HodController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/hod.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.hodController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.add-hod', {
                url: '/add-hod',
                controller: 'HodController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/add-hod.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.hodController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.sms-content', {
                url: '/sms-content',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/sms-content.html';
                },
                authenticate: true
            })
            .state('index.account', {
                url: 'account/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/accounts-internal.html';
                },
                authenticate: true
            })
            .state('index.messages', {
                controller: 'messageController',
                url: 'messages',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    //return 'views/common/messages-test.html';
                    return 'views/common/messages.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.messageController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.messages.compose', {
                url: '/compose',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/compose-mail.html';
                },
                authenticate: true
            })
            .state('index.messages.draft-message', {
                url: '/draft-message/:msgId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/draft-message-details.html';
                },
                authenticate: true
            })
            .state('index.messages.inbox', {
                url: '/inbox',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/message-inbox.html';
                },
                authenticate: true
            })
            .state('index.messages.sent', {
                url: '/sent',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/message-sent.html';
                },
                authenticate: true
            })
            .state('index.messages.draft', {
                url: '/draft',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/message-draft.html';
                },
                authenticate: true
            })
            .state('index.messages.started', {
                url: '/started',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/message-started.html';
                },
                authenticate: true
            })
            .state('index.messages.label', {
                url: '/label/:labelId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/message-label.html';
                },
                authenticate: true
            })
            .state('index.messages.label-message', {
                url: '/label-message/:msgId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/label-message-detail.html';
                },
                authenticate: true
            })
            .state('index.messages.inbox-message', {
                url: '/inbox-message/:msgId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/inbox-message-details.html';
                },
                authenticate: true
            })
            .state('index.messages.sent-message', {
                url: '/sent-message/:msgId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/sent-message-details.html';
                },
                authenticate: true
            })
            .state('index.messages.star-message', {
                url: '/star-message/:msgId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/star-message-details.html';
                },
                authenticate: true
            })
            .state('index.messages.groups', {
                url: '/messages-groups',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/message-groups.html';
                },
                authenticate: true
            })
            .state('index.messages.single-message-group', {
                url: '/messages-group-details/:groupId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/single-message-group-detail.html';
                },
                authenticate: true
            })
            .state('index.messages.add-new-message-group', {
                url: '/add-new-message-group',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/add-new-message-group.html';
                },
                authenticate: true
            })
            .state('index.messages.add-group-member', {
                url: '/add-group-member/:groupId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/add-group-member.html';
                },
                authenticate: true
            })
            .state('index.notifications', {
                url: 'notifications',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/notifications.html';
                },
                authenticate: true
            })
            .state('index.home.add-student', {
                url: '/add-student',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/add-student.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.roles', {
                url: '/roles',
                controller: 'RolesController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/roles.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.rolesController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.user-role-permission', {
                url: '/user-role-permission',
                controller: 'RolesController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/user-role-permission.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.rolesController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.view-user-permissions', {
                url: '/view-user-permissions/:uid',
                controller: 'RolesController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-user-permissions.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.rolesController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.create-question-form', {
                url: '/create-question-form',
                controller: 'MentorController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/create-question-form.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.mentorController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.view-request-detail', {
                url: '/view-request-detail/:id',
                controller: 'AttendanceController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-request-detail.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.attendanceController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.view-branch-students', {
                url: '/view-students',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/view-branch-students.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.user-profile', {
                url: '/user-profile/:uid',
                controller: 'EditProfileController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/view-user-profile.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.editProfileController.js',
                                'angular/ng-controllers/app.NewsFeedController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.settings', {
                url: '/settings',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/settings.html';
                },
                authenticate: true
            })
            .state('index.home.student-fees', {
                url: '/fees',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/student/fees.html';
                },
                authenticate: true
            })
            .state('index.appraisal', {
                url: 'appraisal',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/appraisal.html';
                },
                authenticate: true
            })
            .state('index.appraisal.appraisal-form', {
                url: '/appraisal-form',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/appraisal-forms.html';
                },
                authenticate: true
            })
            .state('index.appraisal.appraisal-form-internal', {
                url: '/appraisal-form-internal',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/appraisal-forms-internal.html';
                },
                authenticate: true
            })
            .state('index.appraisal.appraisal-form-preview', {
                url: '/appraisal-form-preview',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/appraisal-forms-preview.html';
                },
                authenticate: true
            })
            .state('index.home.add-subject', {
                url: '/add-subject',
                controller: 'HodController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/add-subject.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.hodController.js',
                                'angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.assigned-subjects', {
                url: '/assigned-subjects',
                controller: 'HodController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/assigned-subjects.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.hodController.js',
                                'angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.elective-selection', {
                url: '/elective-selection',
                controller: 'StaffController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/elective-selection.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.staffController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.add-session', {
                url: '/add-session',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/add-session.html';
                },
                authenticate: true
            })
            .state('index.home.holidays', {
                url: '/holidays',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/holidays.html';
                },
                authenticate: true
            })
            .state('index.home.reset-admin-password', {
                url: '/reset-password',
                controller: 'LoginController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/reset-admin-password.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.loginController.js']
                        });
                    }]
                },
                authenticate: true
            });

        /***** Routes or states configuration for time table *****/
        /*********************************************************/
        $stateProvider
            .state('index.time-table', {
                url: 'time-table',
                controller: 'TimeTableController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/index.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.TimeTableController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.time-table.create-time-table', {
                url: '/create-time-table',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/create-time-table.html';
                },
                authenticate: true
            })
            .state('index.time-table.student-time-table', {
                url: '/student-time-table',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/time-table.html';
                },
                authenticate: true
            })
            .state('index.time-table.copy-time-table', {
                url: '/copy-time-table',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/copy-time-table.html';
                },
                authenticate: true
            })
            .state('index.time-table.holidays', {
                url: '/holidays',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/holidays.html';
                },
                authenticate: true
            })
            .state('index.time-table.master-time-table', {
                url: '/master-time-table',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/master-time-table.html';
                },
                authenticate: true
            })
            .state('index.time-table.edit-time-table', {
                url: '/edit-time-table/:sessionId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/time-table/edit-time-table.html';
                },
                authenticate: true
            });
        /*********************************************************/
        /***** Routes or states configuration for time table *****/

        /***** Routes or states configuration for attendance *****/
        /*********************************************************/
        $stateProvider
            .state('index.attendance', {
                url: 'attendance',
                controller: 'AttendanceController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/index.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.attendanceController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.attendance.student-attendance', {
                url: '/student-attendance',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/student-attendance.html';
                },
                authenticate: true
            })
            .state('index.attendance.attendance-info', {
                url: '/attendance-info/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/single-lecture-attendance-info.html';
                },
                authenticate: true
            })
            .state('index.attendance.attendance-request', {
                url: '/student-request',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/attendance-request.html';
                },
                authenticate: true
            })
            .state('index.attendance.mark-attendance', {
                url: '/mark/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/attendance-mark.html';
                },
                authenticate: true
            })
            .state('index.attendance.view-attendance', {
                url: '/view/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/attendance-view.html';
                },
                authenticate: true
            })
            .state('index.attendance.take-attendance', {
                url: '/take-attendance',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/take-attendance.html';
                },
                authenticate: true
            })
            .state('index.attendance.pending-attendance', {
                url: '/pending-attendance',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/pending-attendance.html';
                },
                authenticate: true
            })
            .state('index.attendance.pending-attendance-detail', {
                url: '/pending-attendance-details/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/pending-attendance-detail.html';
                },
                authenticate: true
            })
            .state('index.attendance.attendance-approval', {
                url: '/attendance-approval',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/approve-request.html';
                },
                authenticate: true
            })
            .state('index.attendance.view-request-detail', {
                url: '/view-request-detail/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/view-request-detail.html';
                },
                authenticate: true
            })
            .state('index.attendance.attendance-report', {
                url: '/attendance-report',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/attendance-report.html';
                },
                authenticate: true
            })
            .state('index.attendance.extra-attendance', {
                url: '/extra-attendance',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/extra-attendance.html';
                },
                authenticate: true
            })
            .state('index.attendance.sms-to-parent', {
                url: '/sms-to-parent',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/sms-to-parent.html';
                },
                authenticate: true
            })
            .state('index.attendance.sms-to-parent-reports', {
                url: '/sms-to-parent-reports',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/attendance/sms-to-parent-reports.html';
                },
                authenticate: true
            });
        /*********************************************************/
        /***** Routes or states configuration for time table *****/

        /***** Routes or states configuration for mentorship *****/
        /*********************************************************/
        $stateProvider
            .state('index.mentorship', {
                url: 'mentorship',
                controller: 'MentorController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/index.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.mentorController.js', 'angular/ng-controllers/app.busRouteController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.mentorship.assign-mentor', {
                url: '/assign-mentor',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentors.html';
                },
                authenticate: true
            })
            .state('index.mentorship.new-assign-mentor', {
                url: '/assign-mentor/:mentorid',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentors-new.html';
                },
                authenticate: true
            })
            .state('index.mentorship.senior-mentors', {
                url: '/senior-mentors',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/list-of-senior-mentor.html';
                },
                authenticate: true
            })
            .state('index.mentorship.question-from', {
                url: '/question-from',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/create-question-form.html';
                },
                authenticate: true
            })
            .state('index.mentorship.amentor', {
                url: '/mentorship',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentorship.html';
                },
                authenticate: true
            })
            .state('index.mentorship.verify-student', {
                url: '/verify-student/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/verify-student-docs.html';
                },
                authenticate: true
            })
            .state('index.mentorship.schedule-counselling', {
                url: '/schedule-counselling/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/schedule-counselling.html';
                },
                authenticate: true
            })
            .state('index.mentorship.schedule-counseling-date', {
                url: '/schedule-counseling-date?studentId?scheduleId?startDate?endDate',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/schedule-counseling-date.html';
                },
                authenticate: true
            })
            .state('index.mentorship.start-counselling', {
                url: '/start-counselling/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/start-counselling.html';
                },
                authenticate: true
            })
            .state('index.mentorship.start-student-counselling', {
                url: '/start-student-counselling?studentId?scheduleId?formdId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/start-student-counselling.html';
                },
                authenticate: true
            })
            .state('index.mentorship.saved-student-counselling', {
                url: '/saved-student-counselling?studentId?scheduleId?formdId?counsellingDateId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/saved-student-counselling.html';
                },
                authenticate: true
            })
            .state('index.mentorship.create-mentor-question', {
                url: '/create-mentor-question/:formId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/create-mentor-question.html';
                },
                authenticate: true
            })
            .state('index.mentorship.singel-counselling-detail', {
                url: '/single-counselling-detail/:counsellingDateId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/singel-counselling-detail.html';
                },
                authenticate: true
            })
            .state('index.mentorship.student-counselling', {
                url: '/student-counselling',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/student-counselling.html';
                },
                authenticate: true
            })
            .state('index.mentorship.single-student-counselling', {
                url: '/single-student-counselling/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/single-student-counselling.html';
                },
                authenticate: true
            })
            .state('index.mentorship.assign-juniour-mentor', {
                url: '/assign-juniour-mentor/:uid',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/assign-juniour-mentor.html';
                },
                authenticate: true
            })
            .state('index.mentorship.assign-students', {
                url: '/assign-students/:id',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/assign-students.html';
                },
                authenticate: true
            })
            .state('index.mentorship.set-counselling-duration', {
                url: '/set-counselling-duration',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/set-counselling-duration.html';
                },
                authenticate: true
            })
            .state('index.mentorship.follow-up', {
                url: '/follow-up',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/follow-up.html';
                },
                authenticate: true
            })
            .state('index.mentorship.complaint', {
                url: '/complaint',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/complaint.html';
                },
                authenticate: true
            })
            .state('index.mentorship.critical', {
                url: '/critical',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/critical.html';
                },
                authenticate: true
            })
            .state('index.mentorship.mentors-report', {
                url: '/mentors-report',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentors-report.html';
                },
                authenticate: true
            })
            .state('index.mentorship.mentor-report', {
                url: '/mentor-report/:dateId/:mentorId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentor-report.html';
                },
                authenticate: true
            })
            .state('index.mentorship.mentoring-report', {
                url: '/mentoring-report/:counsellingDateId/:mentorId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentoring-report.html';
                },
                authenticate: true
            })
            .state('index.mentorship.mentoring-reports', {
                url: '/mentoring-reports',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentoring-reports.html';
                },
                authenticate: true
            })
            .state('index.mentorship.mentee-reports', {
                url: '/mentee-reports/:counsellingDateId/:mentorId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/mentee-reports.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info', {
                url: '/edit-mentee',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/edit-mentee-info.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info.personal-and-family-info', {
                url: '/personal-and-family-info/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/personal-and-family-info.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info.training-and-placement-details', {
                url: '/training-and-placement-details/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/training-and-placement-details.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info.education-details', {
                url: '/education-details/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/education-details.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info.attendance-details', {
                url: '/attendance-details/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/attendance-details.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info.semester-informations', {
                url: '/semester-informations/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/semester-information.html';
                },
                authenticate: true
            })
            .state('index.mentorship.edit-mentee-info.achievements-and-awards', {
                url: '/achievements-and-awards/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/achievements-and-awards.html';
                },
                authenticate: true
            })
            .state('index.mentorship.assign-route', {
                url: '/assign-route/:studentId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/mentorship/assign-route.html';
                },
                authenticate: true
            });
        /*********************************************************/
        /****** Routes or states configuration for mentorship *****/


        /***** Routes or states configuration for feedback *****/
        /*********************************************************/
        $stateProvider
            .state('index.feedback', {
                url: 'feedback',
                controller: 'FeedbackController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/index.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.feedbackController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.feedback.start-feedback', {
                url: '/start-feedback',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/' + userDetailsProvider.returnUserFolder() + '/start-feedback.html';
                },
                authenticate: true
            })
            .state('index.feedback.my-feedback', {
                url: '/start-feedback',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/my-feedback.html';
                },
                authenticate: true
            })
            .state('index.feedback.send-feedback', {
                url: '/send-feedback',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/send-feedBack.html';
                },
                authenticate: true
            })
            .state('index.feedback.create-feedback-form', {
                url: '/create-feedback-form',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/create-feedback-form.html';
                },
                authenticate: true
            })
            .state('index.feedback.feedback-form-question', {
                url: '/feedback-form-questions/:formId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/feedback-form-question.html';
                },
                authenticate: true
            })
            .state('index.feedback.view-feedback', {
                url: '/view-feedBack/:feedbackId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/view-feedBack.html';
                },
                authenticate: true
            })
            .state('index.feedback.edit-feedback', {
                url: '/edit-feedBack/:feedBackId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/edit-feedBack.html';
                },
                authenticate: true
            })
            .state('index.feedback.student-feedback', {
                url: '/student-feedback/:formId',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/feedback/student-feedBack.html';
                },
                authenticate: true
            })
            /***** Routes or states configuration for feedback *****/
            /*********************************************************/

            /***** Routes or states configuration for bus info *****/
            /*********************************************************/
            .state('index.home.bus', {
                url: '/bus',
                controller: 'BusRouteController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/management/bus.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.busRouteController.js']
                        });
                    }]
                },
                authenticate: true
            })
            .state('index.home.bus.manage-bus-route', {
                url: '/manage-bus-route',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/management/manage-bus-route.html';
                },
                authenticate: true
            })
            .state('index.home.bus.stops', {
                url: '/stops',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/management/stops.html';
                },
                authenticate: true
            })
            .state('index.home.bus.view-bus-route', {
                url: '/view-bus-route/:bus_no',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/management/view-bus-route.html';
                },
                authenticate: true
            })
            .state('index.home.bus.change-users-bus', {
                url: '/change-users-bus',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/management/change-users-bus.html';
                },
                authenticate: true
            })
            .state('index.home.online-users', {
                url: '/online-users',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/common/online-users.html';
                },
                authenticate: true
            })
            /***** Routes or states configuration for bus info *****/
            /*********************************************************/

            .state('index.home.student-attendance', {
                url: '/online-users',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/parent/student-attendance.html';
                },
                authenticate: true
            })
            .state('index.home.child-profile', {
                url: '/child-profile',
                controller: 'ChildProfileController',
                onEnter: function () {
                    windowP.scrollTo(0, 0);
                },
                templateUrl: function () {
                    return 'views/parent/child-profile.html';
                },
                resolve: {
                    onEnter: ['$ocLazyLoad', function ($ocLazyLoad) {
                        return $ocLazyLoad.load({
                            name: 'ecampus',
                            insertBefore: '#ng_load_plugins_before',
                            files: ['angular/ng-controllers/app.ChildProfileController.js']
                        });
                    }]
                },
                authenticate: true
            });
    }

]);

ecampus.controller('AppController', ['$http', '$scope', '$rootScope', 'Storage', '$state', 'Service', 'UserTypes', '$uibModal', 'API', '$q', function ($http, $scope, $rootScope, Storage, $state, Service, UserTypes, $uibModal, API, $q) {

    $rootScope.$on('stateAuth', function (evt, data) {
        if (data.name !== 'login' && data.name !== 'forget-password') {
            Service.authState({'state': data.name.replace('index.', '')}).then(function (res) {
                // Do nothing
            }, function (res) {
                if (!res.data.response) {
                    $state.go('index.home');
                }
            });
        }
    });

    /* regex to validate input over the app */
    $rootScope.regexAll = {};
    $rootScope.regexAll.username = /^[\u00C0-\u1FFF\u2C00-\uD7FF\w]*$/;
    $rootScope.regexAll.fullname = /^[\u00BF-\u1FFF\u2C00-\uD7FF\a-zA-Z ]*$/;
    $rootScope.regexAll.email = /^[_a-zA-Z0-9-]+(\.[_a-zA-Z0-9-]+)*@[a-zA-Z0-9-]+(\.[a-zA-Z0-9-]+)*(\.[a-z]{2,})$/;
    $rootScope.regexAll.address = /^[\u00BF-\u1FFF\u2C00-\uD7FF\a-zA-Z0-9-, ]*$/;
    $rootScope.regexAll.number = /^[0-9]*$/;
    $rootScope.regexAll.contactnumber = /^[0-9+]*$/;
    $rootScope.regexAll.city = /^[\u00BF-\u1FFF\u2C00-\uD7FF\a-zA-Z0-9 ]*$/;

    /* minimum required characters for fields */
    $rootScope.minLength = {};
    $rootScope.minLength.username = 3;
    $rootScope.minLength.password = 6;

    /* maximum required characters for fields */
    $rootScope.maxLength = {};
    $rootScope.maxLength.username = 15;
    $rootScope.maxLength.fullname = 50;
    $rootScope.maxLength.email = 50;
    $rootScope.maxLength.address = 50;
    $rootScope.maxLength.password = 16;
    $rootScope.maxLength.contactnumber = 15;
    $rootScope.maxLength.city = 20;
    $rootScope.maxLength.price = 3;
    $rootScope.maxLength.title = 50;
    $rootScope.maxLength.description = 200;
    $rootScope.maxLength.batch = 2;

    $rootScope.currency = 'Rs.';
    $rootScope.siteLable = 'qualwebs';
    $rootScope.siteTitle = 'eCampus';
    $rootScope.maxAttachmentSize = 10485760; // Size in Bytes

    $scope.tinymceOptions = {
        selector: 'textarea',
        plugins: 'print preview fullpage powerpaste searchreplace autolink directionality advcode visualblocks visualchars fullscreen image link media template codesample table charmap hr pagebreak nonbreaking anchor toc insertdatetime advlist lists textcolor wordcount tinymcespellchecker a11ychecker imagetools mediaembed  linkchecker contextmenu colorpicker textpattern  importcss',
        toolbar1: 'formatselect | bold italic strikethrough forecolor backcolor | link | alignleft aligncenter alignright alignjustify  | numlist bullist outdent indent  | removeformat',
        height: 300,
        branding: false,
        importcss_append: true,
        content_css: [social_url + '/css/tinymce.custom.css']
    };

    /* static messages */
    $rootScope.noNotification = 'You don\'t have any notification';

    $rootScope.accountType = {
        academicStaff: '1',
        adminstration: '2',
        alumni: '3',
        BoG: '4',
        HOD: '5',
        juniorStudent: '6',
        maintenance: '7',
        management: '8',
        mentor: '9',
        NEN: '10',
        nonAcademicStaff: '11',
        parent: '12',
        seniorStudent: '13',
        support: '14',
        admin: '15',
        dean: '16',
        director: '17'
    };

    $scope.achievementTypes = [
        {"value": 3, "text": "Technical Seminar"},
        {"value": 4, "text": "Workshop"},
        {"value": 5, "text": "Competitions"},
        {"value": 1, "text": "Paper & Publications"},
        {"value": 6, "text": "Sports Activities"},
        {"value": 2, "text": "Other"}
    ];

    $scope.sectionArray = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'];


    /* remote-api-handler for angucomplete-alt*/
    $scope.remoteApiHandler = function (searchInput, timeoutPromise) {
        var data = {
            "name": searchInput,
            "limit": 10
        };
        return $http.post(API.get_all_our_user, data, {
            timeout: timeoutPromise
        });
    };

    $scope.selectedPerson = function (user) {
        $state.go('index.home.user-profile', {'uid': user.originalObject.uid});
    };

    /* logout function */
    $scope.clearLocalStorage = function () {
        Storage.clear('ecampus_auth');
        $state.go('login');
        $rootScope.$broadcast('userLoggedIn');
    };

    $scope.goToBack = function () {
        window.history.back();
    };

    $scope.pagination = {};
    $scope.pagination.maxSize = 5;

    /* get all departments */
    $scope.getDepartments = function () {
        Service.getDepartments().then(function (res) {
            $scope.allDepartments = res.data;
        }, function (res) {
            console.log(res);
        });
    };

    $scope.getAccountRoles = function () {
        Service.getAccountTypes().then(function (res) {
            $scope.getUserTypeData = res.data;
        }, function (res) {
            console.log(res);
        });
    };

    $scope.getBranches = function (departmentId) {
        var defer = $q.defer();
        Service.getBranches({'departmentId': departmentId}).then(function (res) {
            $scope.allBranches = res.data;
            defer.resolve();
        }, function (res) {
        });
        return defer.promise;
    };

    $scope.depSubjectObject = {};
    $scope.getDepartmentSubject = function (semId, branchId) {
        $scope.depSubjectObject.semester = semId;
        $scope.depSubjectObject.branchId = branchId;
        Service.getDepartmentSubject($scope.depSubjectObject).then(function (res) {
            $scope.allDepartmentSubjects = res.data.response;
            $scope.getSubjectList();
        }, function () {
            $scope.allDepartmentSubjects = [];
        })
    };


    $scope.getSubjectList = function () {
        $scope.subjectList = [];
        for (var i = 0; i < $scope.allDepartmentSubjects.length; i++) {
            $scope.subjectList.push($scope.allDepartmentSubjects[i].id)
        }
        $scope.subjectObj = JSON.parse(JSON.stringify($scope.subjectList));
    };

    $scope.getUserProfiles = function () {
        Service.getUserProfile().then(function (res) {
            $scope.userProfileData = res.data.response;
            $scope.ProfileData = res.data.response;
            $scope.ProfileData.anniversary = new Date($scope.userProfileData.anniversary);
            $rootScope.profilePicture = res.data.response.image;
            $rootScope.userMentorType = res.data.response.mentorType;
            $rootScope.userId = res.data.response.id;
            $scope.changePicJcrop.imagePath = res.data.response.image;
        }, function (res) {
        });
    };

    $scope.onlyWeekdaysPredicate = function (date) {
        var day = date.getDay();
        return day === 1 || day === 2 || day === 3 || day === 4 || day == 5 || day == 6;
    };

    $scope.today = $scope.newDate;

    $scope.proPicJcrop = {}
    $scope.proPicJcrop.src = '';
    // Must be [x, y, x2, y2, w, h]
    $scope.proPicJcrop.coords = [0, 0, 100, 100, 100, 100];
    $scope.proPicJcrop.imagePath = '/storage/default/user.jpg';

    $scope.changePicJcrop = {}
    $scope.changePicJcrop.src = '';
    // Must be [x, y, x2, y2, w, h]
    $scope.changePicJcrop.coords = [0, 0, 100, 100, 100, 100];
    $scope.changePicJcrop.imagePath = '/storage/default/user.jpg';

    $scope.setImageSrc = function (obj, model, modalId) {
        var reader = new FileReader();
        reader.onload = function (e) {
            obj.src = e.target.result;
            $scope.$apply();
        };
        reader.readAsDataURL(model);
        if (modalId) {
            $('#' + modalId).modal('show');
        } else {
            obj.showCrop = true;
        }
    };

    $scope.uploadProfilePicture = function (obj, model, modalId) {
        if (obj.coords[4] == 0 || obj.coords[5] == 0) {
            swal('Error', 'Select the area to be cropped', 'error');
            return false;
        }
        var fd = new FormData();
        fd.append('file', model);
        fd.append('x', obj.coords[0]);
        fd.append('y', obj.coords[1]);
        fd.append('w', obj.coords[4]);
        fd.append('h', obj.coords[5]);
        obj.disabled = true;
        Service.uploadProfilePicture(fd).then(function (res) {
            obj.imageName = res.data.response.imageName;
            obj.imagePath = res.data.response.imagePath;
            obj.coords = [0, 0, 100, 100, 100, 100];
            if (modalId) {
                $('#' + modalId).modal('hide');
            } else {
                obj.showCrop = false;
            }
            obj.disabled = false;
        }, function (res) {
            obj.disabled = false;
            swal('Error', res.data.message, 'error');
        })
    };

    $scope.getNotifications = function () {
        var flag;
        if ($state.current.name == 'index.notifications') {
            flag = 1;
        } else {
            flag = 0;
        }
        Service.getNotifications(flag).then(function (res) {
            $scope.allNotifications = res.data;
        }, function () {

        });
    };

    $scope.resetNotification = function () {
        Service.resetNotifications().then(function (res) {
            $scope.getNotifications();
        }, function () {

        });
    };

    $scope.getUserRoles = function () {
        Service.userRoles().then(function (res) {
            $scope.userRoles = res.data;
        }, function () {

        });
    };

    $scope.getAccountType = function () {
        $scope.accounType = Storage.get('user_types', true);
        console.log($scope.accounType);
    };

    $scope.addAccountsData = {};
    $scope.addAccounts = function () {
        if ($scope.addAccountsData.disabled) {
            return false;
        }
        if ($scope.proPicJcrop.imageName) {
            $scope.addAccountsData.imageName = $scope.proPicJcrop.imageName;
        }
        $scope.addAccountsData.disabled = true;
        Service.addAccounts($scope.addAccountsData).then(function (res) {
            $scope.addAccountsData.disabled = false;
            $scope.addAccountsData.accountType = "";
            $scope.addAccountsData.firstName = "";
            $scope.addAccountsData.lastName = "";
            $scope.addAccountsData.username = "";
            $scope.addAccountsData.email = "";
            $scope.addAccountsData.gender = "";
            $scope.addAccountsData.branchId = "";
            $scope.addAccountsData.departmentId = "";
            $scope.addAccountsData.section = "";
            $scope.addAccountsData.accountType = "";
            $scope.addAccountsData.batchYear = "";
            $scope.addAccountsData.currentSemester = "";
            $scope.addAccountsData.mobileNo = "";
            swal('Success', res.data.response, 'success');
        }, function (res) {
            $scope.addAccountsData.disabled = false;
            swal('Error', res.data.message, 'error');
        })
    };

    $scope.accountGroups = [];
    $scope.accountGroupsData = {};
    $scope.getAccountGroups = function (accountType) {
        $scope.accountGroupsData.accountType = accountType;
        Service.getAccountGroups($scope.accountGroupsData).then(function (res) {
            $scope.accountGroups = res.data.response;
        }, function (res) {
            $scope.accountGroups = [];
        })
    };

    $scope.editAccountInfoObj = {};
    $scope.editUserDetailModel = function (user) {
        $scope.getAccountGroups(user.accountType);
        $scope.editAccountInfoObj.id = user.id;
        $scope.editAccountInfoObj.firstName = user.firstName;
        $scope.editAccountInfoObj.lastName = user.lastName;
        $scope.editAccountInfoObj.email = user.email;
        $scope.editAccountInfoObj.username = user.username;
        $scope.editAccountInfoObj.enrollNo = user.enrollNo;
        $scope.editAccountInfoObj.accountType = '' + user.accountType + '';
        $scope.editAccountInfoObj.accountStatus = '' + user.accountStatus + '';
        $scope.editAccountInfoObj.groupId = '' + user.groupId + '';
        if (user.department) {
            $scope.editAccountInfoObj.departmentId = user.department[0].departmentId;
            $scope.getBranches($scope.editAccountInfoObj.departmentId);
            $scope.editAccountInfoObj.branchId = user.department[0].branchId;
            $scope.editAccountInfoObj.currentSemester = '' + user.department[0].currentSemester + '';
            $scope.editAccountInfoObj.section = user.department[0].section;
            $scope.editAccountInfoObj.batchYear = user.department[0].batchYear;
            $scope.editAccountInfoObj.batch = user.department[0].batch;
        }
        $('#editUserDetails').modal('show');
    };

    $scope.updateAccountInformations = function () {
        if ($scope.editAccountInfoObj.disabled) {
            return false;
        }
        $scope.editAccountInfoObj.disabled = true;
        Service.updateAccountInformations($scope.editAccountInfoObj).then(function (res) {
            $scope.editAccountInfoObj.disabled = false;
            $scope.getAllOurUsers();
            $('#editUserDetails').modal('hide');
            swal('Success', res.data.response, 'success');
        }, function (res) {
            $scope.editAccountInfoObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };


    $scope.allOurUserData = [];
    $scope.allOurUserObj = {};
    $scope.allOurUserObj.totalItems = "";
    $scope.allOurUserObj.pageNo = 1;
    $scope.allOurUserObj.itemsPerPage = 20;
    $scope.setAllUserPage = function (pageNo) {
        $scope.allOurUserObj.pageNo = pageNo;
    };

    $scope.getAllOurUsers = function () {
        if ($scope.allOurUserObj.disabled) {
            return false;
        }
        $scope.allOurUserObj.disabled = true;
        $scope.allOurUserObj.limit = $scope.allOurUserObj.itemsPerPage;
        Service.getAllOurUsers($scope.allOurUserObj).then(function (res) {
            $scope.allOurUserObj.disabled = false;
            $scope.allOurUserData = res.data.data;
            $scope.allOurUserObj.totalItems = res.data.total;
            resultLength = $scope.allOurUserObj.totalItems;
        }, function (res) {
            $scope.allOurUserObj.disabled = false;
            $scope.allOurUserData = [];
        });
    };


    $scope.confirmToActiveUser = function (user) {
        swal({
            title: 'Are you sure?',
            text: "Do you wants to active this user",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, Active!'
        }).then(function () {
            $scope.activeOrDeactiveUsers(user);
        })
    };

    $scope.confirmToDeactiveUser = function (user) {
        swal({
            title: 'Are you sure?',
            text: "Do you wants to deactive this user",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, Deactive!'
        }).then(function () {
            $scope.activeOrDeactiveUsers(user);
            swal('Error', res.data.message, 'error');
        })
    };

    $scope.activeOrDeactiveUsers = function (user) {
        $scope.user = user;
        $scope.user.accountLoading = true;
        Service.activeOrDeactiveUsers({'id': user.id}).then(function (res) {
            $scope.getAllOurUsers();
            $scope.user.accountLoading = false;
            swal('Success', res.data.response, 'success').then(function () {
            }, function () {
            });
        }, function (res) {
            $scope.user.accountLoading = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.accontTypeData = [];
    $scope.getAccountTypes = function () {
        Service.getAccountType().then(function (res) {
            $scope.accontTypeData = res.data;
        }, function (res) {
            $scope.accontTypeData = [];
        });
    };


    $scope.unreadMsgData = [];
    $scope.getCountOfUnreadMsg = function () {
        Service.countOfUnreadMsg().then(function (res) {
            $scope.unreadMsgData = res.data.response;
        }, function (res) {
            $scope.unreadMsgData = [];
        });
    };

    $scope.suggetionData = {};
    $scope.addSuggetion = function () {
        if ($scope.suggetionData.disabled) {
            return false;
        }
        $scope.suggetionData.disabled = true;
        Service.addSuggetion($scope.suggetionData).then(function (res) {
            $scope.suggetionData.disabled = false;
            $scope.suggetionData.type = "";
            $scope.suggetionData.subject = "";
            $scope.suggetionData.text = "";
            swal('Success', res.data.response, 'success').then(function () {
            }, function () {
            });
        }, function (res) {
            $scope.suggetionData.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.changePasswordData = {};
    $scope.changePassword = function () {
        if ($scope.changePasswordData.disabled) {
            return false;
        }
        $scope.changePasswordData.disabled = true;
        if ($scope.changePasswordData.newPassword != $scope.changePasswordData.confirmNewPassword) {
            swal('Error', 'Password and confirm password not matched!', 'error');
            $scope.changePasswordData.disabled = false;
        } else {
            Service.changePassword($scope.changePasswordData).then(function (res) {
                $scope.changePasswordData.disabled = false;
                $('#settings').modal('hide');
                swal('Success', res.data.response, 'success').then(function () {
                }, function () {
                });
            }, function (res) {
                $scope.changePasswordData.disabled = false;
                $('#settings').modal('hide');
                swal('Error', res.data.message, 'error');
            });
        }
    };

    $scope.suggestionsObj = {};
    $scope.suggestionsObj.totalItems = "";
    $scope.suggestionsObj.pageNo = 1;
    $scope.suggestionsObj.itemsPerPage = 20;
    $scope.setSuggestions = function (pageNo) {
        $scope.suggestionsObj.pageNo = pageNo;
    };

    $scope.getSuggetionData = [];
    $scope.getSuggetions = function () {
        $scope.suggestionsObj.limit = $scope.suggestionsObj.itemsPerPage;
        Service.getSuggetion($scope.suggestionsObj).then(function (res) {
            $scope.getSuggetionData = res.data.response;
            $scope.suggestionsObj.totalItems = res.data.totalCount;
            resultLength = $scope.suggestionsObj.totalItems;
        }, function (res) {
            $scope.getSuggetionData = [];
        })
    };

    $scope.getSingleSuggetionData = [];
    $scope.suggestionData = {};
    $scope.getSingleSuggetion = function () {
        $scope.suggestionData.suggestionId = $state.params.suggetionId;
        Service.getSingleSuggestion($scope.suggestionData).then(function (res) {
            $scope.getSingleSuggetionData = res.data.response;
        }, function (res) {
            $scope.getSingleSuggetionData = [];
        });
    };

    //-----------------------------------------------------------Add session--------------------------------------------------------//

    $scope.addSessionData = {};
    $scope.sessionStartMinDate = moment().toDate();
    $scope.changeDate = function () {
        $scope.sessionEndMinDate = moment($scope.addSessionData.startDate).add(1, "days").toDate();
    };

    $scope.addSession = function () {
        if ($scope.addSessionData.disabled) {
            return false;
        }
        $scope.addSessionData.disabled = true;
        Service.addSession($scope.addSessionData).then(function (res) {
            $scope.addSessionData.disabled = false;
            swal('Success', res.data.response, 'success').then(function () {
            });
            $scope.getSession()
        }, function (res) {
            $scope.addSessionData.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.dateRangeOption = {
        applyClass: 'btn-green',
        locale: {
            applyLabel: "Apply",
            fromLabel: "From",
            format: "DD-MM-YYYY",
            toLabel: "To",
            cancelLabel: 'Cancel',
            customRangeLabel: 'Custom range'
        },
        ranges: {
            'Last 7 Days':
                [moment().subtract(6, 'days'), moment()],
            'Last 30 Days':
                [moment().subtract(29, 'days'), moment()],
            'This Month':
                [moment().startOf('month'), moment().endOf('month')],
            'Last Month':
                [moment().subtract(1, 'month').startOf('month'), moment().subtract(1, 'month').endOf('month')]
        }
    };


    $scope.getSessionData = [];
    $scope.getSession = function () {
        Service.getSession().then(function (res) {
            $scope.getSessionData = res.data.response;
        }, function (res) {
            $scope.getSessionData = [];
        });
    };

    $scope.confirmToRemoveSession = function (sessionId, status) {
        var text;
        if (status) {
            text = 'deactivate'
        } else {
            text = 'activate'
        }
        swal({
            title: 'Are you sure?',
            type: 'question',
            text: 'Do you want to ' + text + ' this session?',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes!'
        }).then(function () {
            $scope.removeSession(sessionId);
        })
    };

    $scope.removeSession = function (sessionId) {
        Service.removeSession({'sessionId': sessionId}).then(function (res) {
            swal('Success', res.data.response, 'success');
            $scope.getSession();
        }, function (res) {
            swal('Error', res.data.message, 'error');
        });
    };


//-----------------------------------------------------------Add session--------------------------------------------------------//

//-----------------------------------------------------------Add holiday--------------------------------------------------------//

    $scope.addHolidayData = {};
    $scope.addHoliday = function () {
        if ($scope.addHolidayData.disabled) {
            return false;
        }
        $scope.addHolidayData.disabled = true;
        Service.addHoliday($scope.addHolidayData).then(function (res) {
            $scope.addHolidayData.disabled = false;
            swal('Success', res.data.response, 'success');
            $scope.getHolidays();
            $scope.addHolidayData.title = "";
            $scope.addHolidayData.holidayDate = "";
        }, function (res) {
            $scope.addHolidayData.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.getHolidaysData = [];
    $scope.getHolidays = function () {
        Service.getHolidays().then(function (res) {
            $scope.getHolidaysData = res.data.response;
        }, function (res) {
            $scope.getHolidaysData = [];
        });
    };

//-----------------------------------------------------------Add holiday--------------------------------------------------------//

    $scope.sixtyDaysTimeStampDaysTimeStamp = 5184000;
    $scope.currentTimeStamp = moment().unix();

    $scope.getAllFaculties = function () {
        Service.getAllFaculties().then(function (res) {
            $scope.allFaculties = res.data.response;
        }, function (res) {
            $scope.allFaculties = [];
        });
    };


    //---------------------------------------------------------logout-----------------------------------------------------------//

    $scope.logoutDisbaled = false;
    $scope.logout = function () {
        if ($scope.logoutDisbaled) {
            return false;
        }
        $scope.logoutDisbaled = true;
        Service.logout().then(function (res) {
            $scope.clearLocalStorage();
            $scope.logoutDisbaled = false;
        });
    };

    //---------------------------------------------------------logout-----------------------------------------------------------//

    //*************function to get server date******************//

    $scope.getServerDate = function () {
        Service.getServerDate().then(function (res) {
            $scope.currentDate = res.data.response.date;
            $scope.newDate = moment(res.data.response.date, 'X').toDate();
            $scope.batchYears = [];
            $scope.passingYears = [];
            var i;
            var obj;
            for (i = 1990; i <= $scope.newDate.getFullYear() + 4; i++) {
                obj = {'year': i};
                $scope.batchYears.push(obj);
                $scope.passingYears.push(obj);
            }
            $scope.birthYear = [];
            for (i = 1990; i <= $scope.newDate.getFullYear(); i++) {
                obj = {'year': i};
                $scope.birthYear.push(obj);
            }
            $scope.eligibleYear = [];
            for (i = 2010; i <= $scope.newDate.getFullYear() + 1; i++) {
                obj = {'year': i};
                $scope.eligibleYear.push(obj);
            }
            $scope.currentTimeZone = res.data.response.timezone;
            moment.tz.setDefault($scope.currentTimeZone);
        });
    };

    //*************function to get server date******************//

    $scope.getSchoolBoardsData = []
    $scope.getSchoolBoards = function () {
        Service.getSchoolBoards().then(function (res) {
            $scope.getSchoolBoardsData = res.data.response;
        }, function (res) {
            $scope.getSchoolBoardsData = []
        });
    };


    //--------------------------------------------------------logout ideal system------------------------------------------------//

    //--------------------------------------------------eligible students---------------------------------------------------//

    $scope.checkEliData = [];
    $scope.checkEligibility = function () {
        Service.checkEligibility().then(function (res) {
            if (res.data.response == true) {
                $('#studentConfirmation').modal({backdrop: 'static', keyboard: false});
            }
            $scope.checkEliData = res.data.circularDetails;
        });
    };

    $scope.checkSelection = function () {
        Service.checkSelection().then(function (res) {
            if (res.data.response == true) {
                $('#confirmStundentJoining').modal({backdrop: 'static', keyboard: false});
            }
            $scope.checkStdSelection = res.data.circularDetails;
        });
    };

    $scope.interestObj = {};
    $scope.submitInterest = function (circularId) {
        if ($scope.interestObj.disabled) {
            return false;
        }
        $scope.interestObj.circularId = circularId;
        $scope.interestObj.disabled = true;
        Service.submitInterest($scope.interestObj).then(function (res) {
            $scope.interestObj.disabled = false;
            $('#studentConfirmation').modal('hide');
            swal('Success', res.data.response, 'success');
        }, function (res) {
            $scope.interestObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.joiningObj = {};
    $scope.submitJoiningConfirmation = function (circularId) {
        if ($scope.joiningObj.disabled) {
            return false;
        }
        $scope.joiningObj.circularId = circularId;
        $scope.joiningObj.disabled = true;
        Service.submitJoiningConfirmation($scope.joiningObj).then(function (res) {
            $scope.joiningObj.disabled = false;
            $('#confirmStundentJoining').modal('hide')
            $scope.checkSelection();
            swal('Success', res.data.response, 'success');
        }, function (res) {
            $scope.joiningObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    //--------------------------------------------------eligible students---------------------------------------------------//

    //--------------------------------------------------Students fees---------------------------------------------------//

    $scope.studentFeesData = [];
    $scope.studentFeesList = function () {
        Service.studentFeesList().then(function (res) {
            $scope.studentFeesData = res.data.response;
            var dr = 0;
            var cr = 0;
            angular.forEach($scope.studentFeesData, function (v, i) {
                dr += parseInt(v['Amount Dr']);
                cr += parseInt(v['Amount Cr']);
            });
            $scope.feesBalance = dr - cr;
        });
    };

    //--------------------------------------------------Students fees---------------------------------------------------//

    //--------------------------------------------------get library url---------------------------------------------------//

    $scope.getLibraryUrl = function () {
        Service.getLibraryUrl().then(function (res) {
            window.location.href = res.data.response.url
        });
    };

    //--------------------------------------------------Get SMS Content Or Edit---------------------------------------------------//

    $scope.listOfSmsContent = [];
    $scope.getSmsContent = function () {
        Service.getSmsContent().then(function (res) {
            $scope.listOfSmsContent = res.data.response;
        }, function (res) {
            $scope.listOfSmsContent = [];
        });
    };

    $scope.smsContentObj = {};
    $scope.openSMSContentModal = function (sms) {
        $scope.smsContentObj.sms_content = sms.sms_content;
        $scope.smsContentObj.id = sms.id;
        $scope.smsContentObj.active = sms.active;
        $('#editSmsModal').modal('show');
    };

    $scope.editSmsContent = function () {
        if ($scope.smsContentObj.disabled) {
            return false;
        }
        $scope.smsContentObj.disabled = true;
        Service.editSmsContent($scope.smsContentObj).then(function (res) {
            swal({
                type: 'success',
                title: 'Success',
                text: res.data.response,
                timer: 1500
            });
            $scope.smsContentObj.disabled = false;
            $('#editSmsModal').modal('hide');
            $scope.getSmsContent();
        }, function (res) {
            swal('Error', res.data.message, 'error');
            $scope.smsContentObj.disabled = false;
        });
    };

    $scope.noticeData = {};
    $scope.noticeData.active = '0';
    $scope.noticeData.disabled = false;

    $scope.getSiteNotice = function () {
        if ($scope.noticeData.disabled) {
            return false;
        }
        $scope.noticeData.disabled = true;
        Service.getSiteNotice().then(function (res) {
            if (res.data.response.length) {
                $scope.noticeData.txt = res.data.response[0].label;
                $scope.noticeData.active = '' + res.data.response[0].value + '';
                if (res.data.response[0].value == 1) {
                    $scope.displayNotice = res.data.response[0].label;
                }
            }
            $scope.noticeData.disabled = false;
        }, function (res) {
            $scope.noticeData.disabled = false;
            swal("Error", res.message, "error");
        });
    };

    $scope.getAttendanceComments = function () {
        Service.getAttendanceComments().then(function (res) {
            $scope.attendanceComments = res.data.response;
        }, function (res) {

        })
    };

    $scope.addAttendanceData = {};
    $scope.addAttendanceComment = function () {
        if ($scope.addAttendanceData.disabled) {
            return false;
        }
        $scope.addAttendanceData.disabled = true;
        Service.addAttendanceComment($scope.addAttendanceData).then(function (res) {
            $scope.addAttendanceData.disabled = false;
            $scope.addAttendanceData.comment = '';
            $scope.getAttendanceComments();
            swal("Success", res.data.response, "success");
        }, function (res) {
            $scope.addAttendanceData.disabled = false;
            swal("Error", res.message, "error");
        });
    };

    $scope.removeAttendanceComment = function (id) {
        Service.deleteAttendanceComment({'commentId': id}).then(function (res) {
            $scope.getAttendanceComments();
            swal("Success", res.data.response, "success");
        }, function (res) {
            swal("Error", res.message, "error");
        })
    };

    setTimeout(function () {
        $scope.getSiteNotice();
    }, 5000);

    $scope.updateSiteNotice = function () {
        if ($scope.noticeData.disabled) {
            return false;
        }
        $scope.noticeData.disabled = true;
        Service.updateSiteNotice($scope.noticeData).then(function (res) {
            $scope.noticeData.disabled = false;
            swal("Success", res.response, "success");
        }, function (res) {
            $scope.noticeData.disabled = false;
            swal("Error", res.message, "error");
        })
    };


    function notify(data) {
        //---------------------------------generate notification box------------------------------------------------//
        $.notify({
            icon: $rootScope.base_url + data.icon,
            title: data.title,
            message: data.message
        }, {
            type: 'minimalist',
            delay: 5000,
            icon_type: 'image',
            template: '<div data-notify="container" class="col-xs-11 col-sm-3 alert alert-{0}" role="alert">' +
                '<img data-notify="icon" class="img-circle pull-left">' +
                '<span data-notify="title">{1}</span>' +
                '<span data-notify="message">{2}</span>' +
                '</div>'
        });
    }

    function notify_broadcast(data) {
        //---------------------------------generate notification box------------------------------------------------//
        $.notify({
            icon: $rootScope.base_url + data.icon_broadcast,
            title: data.title_broadcast,
            message: data.msg_broadcast
        }, {
            type: 'minimalist',
            delay: 500000,
            icon_type: 'image',
            template: '<div data-notify="container" class="col-xs-11 col-sm-3 alert alert-{0}" role="alert">' +
                '<img data-notify="icon" class="img-circle pull-left">' +
                '<span data-notify="title">{1}</span>' +
                '<span data-notify="message">{2}</span>' +
                '</div>'
        });
    }


    //--------------------------------------------------Get SMS Content Or Edit---------------------------------------------------//
    socket.on('message', function (data) {
        if (Storage.has('ecampus_auth') && Storage.get('ecampus_auth', true).id) {
            var d = JSON.parse(data);
            if (d.id == Storage.get('ecampus_auth', true).id) {
                $scope.getCountOfUnreadMsg();
                if ($state.current.name == 'index.messages.inbox') {
                    $rootScope.$broadcast('getInbox');
                }
            }
        }
    });

    socket.on('news-feed', function (data) {
        if (Storage.has('ecampus_auth') && Storage.get('ecampus_auth', true).id) {
            var d = JSON.parse(data);
            if ($state.current.name == 'index.home.news-feeds') {
                $rootScope.$broadcast('news_feeds');
            }
            /*if (d.id == Storage.get('ecampus_auth', true).id) {
                notify(d);
            }
            else {
                notify_broadcast(d);
            }*/
        }

    });

    socket.on('notification', function (data) {
        if (Storage.has('ecampus_auth') && Storage.get('ecampus_auth', true).id) {
            var d = JSON.parse(data);
            if (d.id == Storage.get('ecampus_auth', true).id) {
                $scope.getNotifications();
            }
        }

    });

    socket.on('presence', function (data) {
        if (Storage.has('user_socket_id')) {
            socket.emit('update_list', {'id': Storage.get('user_socket_id')});
        }
        Storage.set('user_socket_id', data.id);
        $rootScope.$broadcast('userLoggedIn');
    });

    socket.on('online', function (data) {
        $scope.$apply(function () {
            $scope.onlineUsers = data;
        });
    });

    $rootScope.$on('userLoggedIn', function () {
        if (Storage.has('ecampus_auth')) {
            socket.emit('new_user', {
                'id': Storage.get('user_socket_id'),
                'user_id': Storage.get('ecampus_auth', true).id,
                'full_name': Storage.get('ecampus_auth', true).fullname,
                'username': Storage.get('ecampus_auth', true).username,
                'type': Storage.get('ecampus_auth', true).type
            });
        } else {
            socket.emit('new_user', {'id': Storage.get('user_socket_id')});
        }
    });

    $scope.select2Options = {
        allowClear: true
    };

    $scope.renderedTrue = function () {
        $rootScope.newsFeedRendered = true;
    }

}]);

ecampus.config(['$qProvider', function ($qProvider) {
    $qProvider.errorOnUnhandledRejections(false);
}]);

ecampus.config(function ($mdDateLocaleProvider) {

    $mdDateLocaleProvider.formatDate = function (date) {
        if (!date) {
            return '';
        } else {
            return moment(date).format('DD-MM-YYYY');
        }
    };

    $mdDateLocaleProvider.parseDate = function (dateString) {
        var m = moment(dateString, 'DD-MM-YYYY', true);
        return m.isValid() ? m.toDate() : new Date(NaN);
    };

});

ecampus.config(['momentPickerProvider', function (momentPickerProvider) {
    momentPickerProvider.options({
        minutesStep: 1
    });
}]);

function setModalMaxHeight(element) {
    this.$element = $(element);
    this.$content = this.$element.find('.modal-content');
    this.$content.css({
        'overflow': 'hidden'
    });
}

$('.modal').on('show.bs.modal', function () {
    $(this).show();
    setModalMaxHeight(this);
});

function showMessage(ele) {
    var display = $(ele).parent().parent().find('div.forward-message-body').first().css('display');
    if (display == 'block') {
        $(ele).parent().parent().find('div.forward-message-body').first().css('display', 'none');
    } else {
        $(ele).parent().parent().find('div.forward-message-body').first().css('display', 'block');
    }
}

function readMoreNews(e) {
    var ele = $(e).parent('.news-feed-more').find('.content');
    ele.css('height', 'auto');
    ele.css('overflow', 'unset');
    $(e).parent('.news-feed-more').find('.read-more').css('display', 'none');
    $(e).parent('.news-feed-more').find('.read-less').css('display', 'block');

}

function readLessNews(e) {
    var ele = $(e).parent('.news-feed-more').find('.content');
    ele.css('height', '300px');
    ele.css('overflow', 'hidden');
    $(e).parent('.news-feed-more').find('.read-less').css('display', 'none');
    $(e).parent('.news-feed-more').find('.read-more').css('display', 'block');
}
