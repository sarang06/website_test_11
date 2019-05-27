var componentForm = {};
componentForm.street_number = 'short_name';
componentForm.route = 'long_name';
componentForm.locality = 'long_name';
componentForm.administrative_area_level_1 = 'short_name';
componentForm.country = 'long_name';
componentForm.postal_code = 'short_name';
var base = window.location.protocol + '//localhost/ecampus/';
angular.module('ecampus')
    .directive('googlePlace', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attrs, ngModel) {
                var options = {
                    types: ['(cities)']
                };
                g_country = new google.maps.places.Autocomplete(element[0], options);
                google.maps.event.addListener(g_country, 'place_changed', function () {
                    var geoComponents = g_country.getPlace();
                    if (geoComponents) {
                        for (var i = 0; i < geoComponents.address_components.length; i++) {
                            if (geoComponents.address_components[i].types[0] == 'locality') {
                                scope.$apply(function () {
                                    ngModel.$setViewValue(geoComponents.address_components[i].long_name);
                                    ngModel.$render();
                                });
                            }
                        }
                    }
                });
                element.bind("keypress", function (event) {
                    var keyCode = event.which || event.keyCode;
                    if (keyCode == 13) {
                        event.preventDefault();
                    }
                });
            }
        };
    })
    .directive('googleAuto', function () {
        return {
            require: 'ngModel',
            scope: {
                inputChange: '='
            },
            link: function (scope, element, attrs, ngModel) {
                var options = {
                    types: [],
                    componentRestrictions: {country: 'in'}
                };
                place = new google.maps.places.Autocomplete(element[0], options);
                google.maps.event.addListener(place, 'place_changed', function () {
                    var geoComponents = place.getPlace();
                    var lat = geoComponents.geometry.location.lat();
                    var lng = geoComponents.geometry.location.lng();
                    scope.inputChange({latitude: lat, longitude: lng});
                });
                element.bind("keypress", function (event) {
                    var keyCode = event.which || event.keyCode;
                    if (keyCode == 13) {
                        event.preventDefault();
                    }
                });
            }
        };
    })
    .directive('onFinishRender', function ($timeout) {
        return {
            restrict: 'A',
            scope: {
                repeatAction: '&'
            },
            link: function (scope, element) {
                var elemScope = element.scope();
                if (elemScope.$last === true) {
                    $timeout(function () {
                        scope.$emit('ngRepeatFinished');
                        scope.repeatAction();
                    });
                }
            }
        };
    })
    .directive('numberInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9]/g, '');
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('fileModel', ['$parse', function ($parse) {
        return {
            restrict: 'A',
            link: function (scope, element, attrs) {
                var model, modelSetter;

                attrs.$observe('fileModel', function () {
                    model = $parse(attrs.fileModel);
                    modelSetter = model.assign;
                });

                element.bind('change', function () {
                    scope.$apply(function () {
                        modelSetter(scope.$parent, element[0].files[0]);
                        scope.$eval(attrs.action);
                    });
                });
            }
        };
    }])
    .directive('fileModel2', ['$parse', function ($parse) {
        return {
            restrict: 'A',
            link: function (scope, element, attrs) {
                var model, modelSetter;

                attrs.$observe('fileModel2', function () {
                    model = $parse(attrs.fileModel2);
                    modelSetter = model.assign;
                });

                element.bind('change', function () {
                    scope.$apply(function () {
                        modelSetter(scope.$parent.$parent, element[0].files[0]);
                        scope.$eval(attrs.action);
                    });
                });
            }
        };
    }])
    .directive('contactInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9+]/g, '');
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('batchInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9a-zA-Z]/g, '');
                    formedInput = formedInput.substr(0, 2);
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('criteriaInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9a-zA-Z,]/g, '');
                    formedInput = formedInput.substr(0, 2);
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('persentInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9.]/g, '');
                    formedInput = formedInput.substr(0, 5);
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('timeInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9]/g, '');
                    formedInput = formedInput.substr(0, 2);
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    /* .directive('tnpPakageInput', function () {
         return {
             require: 'ngModel',
             link: function (scope, element, attr, ngModel) {
                 function fromUser(text) {
                     var formedInput = text.replace(/[^0-9,]/g, '');
                     formedInput = formedInput.substr(0, 8);
                     var tnpPackage = [];
                     for (var i = 0; i < formedInput.length; i++) {
                         tnpPackage.push(formedInput[i]);
                     }
                     angular.forEach(tnpPackage, function (v, k) {
                         if (k == 0 && tnpPackage[k] == ',') {
                             tnpPackage.splice(0, 1);
                         }
                         else if (k == 1 && tnpPackage[k] == ',') {
                             tnpPackage.splice(1, 1);
                         }
                         else if (k == 2 && tnpPackage[k] != ',') {
                             var d = tnpPackage[k];
                             tnpPackage.splice(2, 1, ',', d);
                         } else if (k == 3 && tnpPackage[k] == ',') {
                             tnpPackage.splice(3, 1, 0);
                         } else if (k == 4 && tnpPackage[k] == ',') {
                             tnpPackage.splice(4, 1, 0);
                         } else if (k == 5 && tnpPackage[k] == ',') {
                             tnpPackage.splice(5, 1, 0);
                         } else if (k == 6 && tnpPackage[k] != ',') {
                             var d = tnpPackage[k];
                             tnpPackage.splice(6, 1, ',', d);
                         } else if (k == 7 && tnpPackage[k] == ',') {
                             tnpPackage.splice(7, 1, 0);
                         }
                     });
                     formedInput = tnpPackage.join('');
                     if (formedInput !== text) {
                         ngModel.$setViewValue(formedInput);
                         ngModel.$render();
                     }
                     return formedInput;
                 }
                 ngModel.$parsers.push(fromUser);
             }
         };
     })*/
    /* .directive('tnpPakageInput', function () {
         return {
             require: 'ngModel',
             link: function (scope, element, attr, ngModel) {
                 function fromUser(text) {
                     var formedInput = text.replace(/[^0-9,]/g, '');
                     formedInput = formedInput.substr(0, 8);
                     var tnpPackage = [];
                     for (var i = 0; i < formedInput.length; i++) {
                         tnpPackage.push(formedInput[i]);
                     }
                     angular.forEach(tnpPackage, function (v, k) {
                         if (k == 0 && tnpPackage[k] == ',') {
                             tnpPackage.splice(0, 1);
                         }
                         else if (k == 1 && tnpPackage[k] == ',') {
                             tnpPackage.splice(1, 1);
                         }
                         else if (k == 2 && tnpPackage[k] != ',') {
                             var d = tnpPackage[k];
                             tnpPackage.splice(2, 1, ',', d);
                         } else if (k == 3 && tnpPackage[k] == ',') {
                             tnpPackage.splice(3, 1, 0);
                         } else if (k == 4 && tnpPackage[k] == ',') {
                             tnpPackage.splice(4, 1, 0);
                         } else if (k == 5 && tnpPackage[k] == ',') {
                             tnpPackage.splice(5, 1, 0);
                         } else if (k == 6 && tnpPackage[k] != ',') {
                             var d = tnpPackage[k];
                             tnpPackage.splice(6, 1, ',', d);
                         } else if (k == 7 && tnpPackage[k] == ',') {
                             tnpPackage.splice(7, 1, 0);
                         }
                     });
                     formedInput = tnpPackage.join('');
                     if (formedInput !== text) {
                         ngModel.$setViewValue(formedInput);
                         ngModel.$render();
                     }
                     return formedInput;
                 }
                 ngModel.$parsers.push(fromUser);
             }
         };
     })*/
    .directive('tnpPakageInput', function ($filter) {
        return {
            require: 'ngModel',
            link: function (scope, elem, attrs, ngModelCtrl) {

                ngModelCtrl.$formatters.push(function (modelValue) {
                    return setDisplayNumber(modelValue, true);
                });

                // it's best to change the displayed text using elem.val() rather than
                // ngModelCtrl.$setViewValue because the latter will re-trigger the parser
                // and not necessarily in the correct order with the changed value last.
                // see http://radify.io/blog/understanding-ngmodelcontroller-by-example-part-1/
                // for an explanation of how ngModelCtrl works.
                ngModelCtrl.$parsers.push(function (viewValue) {
                    setDisplayNumber(viewValue);
                    return setModelNumber(viewValue);
                });

                // occasionally the parser chain doesn't run (when the user repeatedly
                // types the same non-numeric character)
                // for these cases, clean up again half a second later using "keyup"
                // (the parser runs much sooner than keyup, so it's better UX to also do it within parser
                // to give the feeling that the comma is added as they type)
                elem.bind('keyup focus', function () {
                    setDisplayNumber(elem.val());
                });

                function setDisplayNumber(val, formatter) {
                    var valStr, displayValue;

                    if (typeof val === 'undefined') {
                        return;
                    }

                    valStr = val.toString();
                    displayValue = valStr.replace(/,/g, '').replace(/[A-Za-z]/g, '');
                    displayValue = displayValue.substr(0, 8);
                    displayValue = parseFloat(displayValue);
                    displayValue = (!isNaN(displayValue)) ? displayValue.toString() : '';

                    // handle leading character -/0
                    if (valStr.length === 1 && valStr[0] === '-') {
                        displayValue = valStr[0];
                    } else if (valStr.length === 1 && valStr[0] === '0') {
                        displayValue = '';
                    } else {
                        displayValue = $filter('number')(displayValue);
                    }

                    if (attrs.positive && displayValue[0] === '-') {
                        displayValue = displayValue.substring(1);
                    }

                    if (typeof formatter !== 'undefined') {
                        return (displayValue === '') ? 0 : displayValue;
                    } else {
                        elem.val((displayValue === '0') ? '' : displayValue);
                    }
                }

                function setModelNumber(val) {
                    var modelNum = val.toString().replace(/,/g, '').replace(/[A-Za-z]/g, '');
                    modelNum = parseFloat(modelNum);
                    modelNum = (!isNaN(modelNum)) ? modelNum : 0;
                    if (modelNum.toString().indexOf('.') !== -1) {
                        modelNum = Math.round((modelNum + 0.00001) * 100) / 100;
                    }
                    if (attrs.positive) {
                        modelNum = Math.abs(modelNum);
                    }
                    return modelNum;
                }
            }
        };
    })
    .directive('sgpaInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9.]/g, '');
                    formedInput = formedInput.substr(0, 4).toString();
                    var sgpaPercent = [];
                    for (var i = 0; i < formedInput.length; i++) {
                        sgpaPercent.push(formedInput[i]);
                    }
                    angular.forEach(sgpaPercent, function (v, k) {
                        if (k == 0 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(0, 1);
                        }
                        else if (k == 1 && sgpaPercent[k] != '.') {
                            var d = sgpaPercent[k];
                            sgpaPercent.splice(1, 1, '.', d);
                        } else if (k == 2 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(2, 1, 0);
                        } else if (k == 3 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(3, 1, 0);
                        }
                    });
                    formedInput = sgpaPercent.join('');
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('eduPercentInput', function () {
        return {
            require: 'ngModel',
            link: function (scope, element, attr, ngModel) {
                function fromUser(text) {
                    var formedInput = text.replace(/[^0-9.]/g, '');
                    formedInput = formedInput.substr(0, 5).toString();
                    var sgpaPercent = [];
                    for (var i = 0; i < formedInput.length; i++) {
                        sgpaPercent.push(formedInput[i]);
                    }
                    angular.forEach(sgpaPercent, function (v, k) {
                        if (k == 0 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(0, 1);
                        }
                        if (k == 1 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(1, 1);
                        }
                        else if (k == 2 && sgpaPercent[k] != '.') {
                            var d = sgpaPercent[k];
                            sgpaPercent.splice(2, 1, '.', d);
                        }
                        else if (k == 3 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(3, 1, 0);
                        }
                        else if (k == 4 && sgpaPercent[k] == '.') {
                            sgpaPercent.splice(4, 1, 0);
                        }
                    });
                    formedInput = sgpaPercent.join('');
                    if (formedInput !== text) {
                        ngModel.$setViewValue(formedInput);
                        ngModel.$render();
                    }
                    return formedInput;
                }

                ngModel.$parsers.push(fromUser);
            }
        };
    })
    .directive('button', function () {
        return {
            restrict: 'E',
            scope: {
                ngDisabled: '='
            },
            link: function (scope, element, attr) {
                var text = element.html();
                scope.$watch(function () {
                    return scope.ngDisabled;
                }, function (val) {
                    if (!val) {
                        element.html(text);
                    }
                });
                element.on('click', function (e) {
                    scope.$apply(function () {
                        setTimeout(function () {
                            if (scope.ngDisabled) {
                                element.html('Loading...');
                            }
                        }, 50);
                    });
                });
            }
        };
    })
    .directive('ngEnter', function () {
        return function (scope, element, attrs) {
            element.bind("keydown keypress", function (event) {
                if (event.which === 13) {
                    scope.$apply(function () {
                        scope.$eval(attrs.ngEnter);
                    });

                    event.preventDefault();
                }
            });
        };
    })
    .directive('niceScroll', [function () {
        return {
            restrict: 'A',
            link: function (scope, element) {

                scope.niceScroll = function (selector, color, cursorWidth) {
                    $(selector).niceScroll({
                        cursorcolor: color,
                        cursorborder: 0,
                        cursorborderradius: 0,
                        cursorwidth: cursorWidth,
                        bouncescroll: true,
                        mousescrollstep: 100,
                    });
                };

                //Scrollbar for HTML(not mobile) but not for login page
                if (!$('html').hasClass('ismobile')) {
                    if (!$('.login-content')[0]) {
                        scope.niceScroll('html', '#00adef', '5px');
                    }

                    //Scrollbar Tables
                    if ($('.table-responsive')[0]) {
                        scope.niceScroll('.table-responsive', '#00adef', '5px');
                    }

                    //Scrill bar for Chosen
                    if ($('.scroll')[0]) {
                        scope.niceScroll('.scroll', '#00adef', '5px');
                    }
                }
            }
        }
    }])

    .directive('checkImage', function ($q) {
        return {
            restrict: 'A',
            link: function (scope, element, attrs) {
                attrs.$observe('ngSrc', function (ngSrc) {
                    var deferred = $q.defer();
                    var image = new Image();
                    image.onerror = function () {
                        deferred.resolve(false);
                        element.attr('src', base + '/images/default.png'); // set default image
                    };
                    image.onload = function () {
                        deferred.resolve(true);
                    };
                    image.src = ngSrc;
                    return deferred.promise;
                });
            }
        }
    })
    .directive('autoFocus', function ($timeout) {
        return {
            restrict: 'AC',
            link: function (_scope, _element) {
                $timeout(function () {
                    _element[0].focus();
                }, 0);
            }
        };
    })
    .directive('newsFeedMore', function ($timeout, $rootScope) {
        return {
            restrict: 'C',
            link: function (scope, element) {
                $rootScope.$watch('newsFeedRendered', function (newVal) {
                    if (newVal) {
                        if ($(element).outerHeight() > 300) {
                            $(element).find('.read-more').css('display', 'block');
                            var ele = $(element).find('.content');
                            ele.css('height', '300px');
                            ele.css('overflow', 'hidden');
                        }
                    }
                });
            }
        };
    });
