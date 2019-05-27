angular.module('ecampus')
    .filter('hasState', function () {
        return function (value, state) {
            if (!value) {
                return false;
            }
            if (value.indexOf(state) != -1) {
                return true;
            } else {
                return false;
            }
        };
    })

    .filter('hasStateRestrict', function () {
        return function (value, state) {
            if (!value) {
                return false;
            }
            if (state == value) {
                return true;
            } else {
                return false;
            }
        };
    })

    .filter('maritalStatus', function () {
        return function (value) {
            if (value == '0') {
                return 'Unmarried';
            }
            if (value == '1') {
                return 'Married';
            }
        };
    })

    .filter('dirMod', function () {
        return function (value) {
            if (value == 'Administration') {
                return 'DIR';
            }
            else {
                return value;
            }
        };
    })

    .filter('gender', function () {
        return function (value) {
            if (value == '1') {
                return 'Male';
            }
            if (value == '2') {
                return 'Female';
            }
        };
    })

    .filter('weekday', function () {
        return function (val) {
            if (val == 0) {
                return 'MON'
            }
            ;
            if (val == 1) {
                return 'TUE'
            }
            ;
            if (val == 2) {
                return 'WED'
            }
            ;
            if (val == 3) {
                return 'THU'
            }
            ;
            if (val == 4) {
                return 'FRI'
            }
            ;
            if (val == 5) {
                return 'SAT'
            }
            ;
        }
    })

    .filter('assignDay', function () {
        return function (val) {
            if (val == 1) {
                return 'Monday'
            }
            if (val == 2) {
                return 'Tuesday'
            }
            if (val == 3) {
                return 'Wednesday'
            }
            if (val == 4) {
                return 'Thursday'
            }
            if (val == 5) {
                return 'Friday'
            }
            if (val == 6) {
                return 'Saturday'
            }
        }
    })

    .filter('unsafe', function ($sce) {
        return $sce.trustAsHtml;
    })

    .filter('privacyStatus', function () {
        return function (value) {
            if (value == '0') {
                return 'Public';
            }
            if (value == '1') {
                return 'Private';
            }
        };
    })

    .filter('grievanceStatus', function () {
        return function (value) {
            if (value == '0') {
                return 'Pending';
            }
            if (value == '1') {
                return 'Followup';
            }
            if (value == '2') {
                return 'Resolved';
            }
            if (value == '3') {
                return 'Disposed';
            }
        };
    })
 .filter('remarkStatus', function () {
        return function (value) {
            if (value == '') {
                return 'NA';
            }
            else {
                return value;
            }

        };
    })

    .filter('explodeAttachment', function () {
        return function (value) {
            if (value!='') {
                value = value.split('+');
                return value[1];
            }
        };
    })


    .filter('toDate', function () {
        return function (input) {
            return new Date(input);
        }
    })

    .filter('removeHtml', function () {
        return function (text) {
            return text ? String(text).replace(/<[^>]+>/gm, '') : '';
        };
    })

    .filter('mentorType', function () {
        return function (value) {
            if (value == '1') {
                return 'Mentor';
            } else if (value == '2') {
                return 'Senior Mentor';
            } else if (value == '3') {
                return 'Deputy Chief Mentor';
            } else if (value == '4') {
                return 'Joint Chief Mentor';
            } else if (value == '5') {
                return 'Chief Mentor';
            } else {
                return '';
            }
        };
    })

    .filter('attandance', function () {
        return function (value) {
            if (value == '1') {
                return 'Present';
            }
            else if (value == '2') {
                return 'Absent';
            }
            else {
                return value;
            }
        };
    })

    .filter('requestStatus', function () {
        return function (value) {
            if (value == '1') {
                return 'Pending';
            }
            if (value == '2') {
                return 'Approved';
            }
            if (value == '3') {
                return 'Declined';
            }
        };
    })

    .filter('department', function () {
        return function (value) {
            if (value == '1') {
                return 'BE';
            }
            if (value == '2') {
                return 'CDIPS';
            }
        };
    })

    .filter('semester', function () {
        return function (value) {
            if (value == '1') {
                return '1st';
            }
            if (value == '2') {
                return '2nd';
            }
            if (value == '3') {
                return '3rd';
            }
            if (value == '4') {
                return '4th';
            }
            if (value == '5') {
                return '5th';
            }
            if (value == '6') {
                return '6th';
            }
            if (value == '7') {
                return '7th';
            }
            if (value == '8') {
                return '8th';
            } else {
                return value;
            }
        };
    })

    .filter('semInRoman', function () {
        return function (value) {
            if (value == '1') {
                return 'I';
            }
            if (value == '2') {
                return 'II';
            }
            if (value == '3') {
                return 'III';
            }
            if (value == '4') {
                return 'IV';
            }
            if (value == '5') {
                return 'V';
            }
            if (value == '6') {
                return 'VI';
            }
            if (value == '7') {
                return 'VII';
            }
            if (value == '8') {
                return 'VIII';
            }
        };
    })

    .filter('suggetionType', function () {
        return function (value) {
            if (value == '1') {
                return 'Idea';
            }
            if (value == '2') {
                return 'Feedback';
            }
            if (value == '3') {
                return 'Suggestion';
            }
        };
    })

    .filter('companyStatus', function () {
        return function (value) {
            if (value == '0') {
                return 'Saved';
            }
            if (value == '1') {
                return 'Saved';
            }
            if (value == '2') {
                return 'Approved';
            }
            if (value == '3') {
                return 'Rejected';
            }
        };
    })

    .filter('companyStatusLabel', function () {
        return function (value) {
            if (value == '0') {
                return 'label-warning';
            }
            if (value == '1') {
                return 'label-warning';
            }
            if (value == '2') {
                return 'label-success';
            }
            if (value == '3') {
                return 'label-danger';
            }
        };
    })

    .filter('consultancyStatus', function () {
        return function (value) {
            if (value == '0') {
                return 'Pending';
            }
            if (value == '1') {
                return 'Active';
            }
        };
    })

    .filter('consultancyStatusLabel', function () {
        return function (value) {
            if (value == '0') {
                return 'label-danger';
            }
            if (value == '1') {
                return ' label-success';
            }
        };
    })

    .filter('campusType', function () {
        return function (value) {
            if (value == '1') {
                return 'Closed Campus';
            }
            if (value == '2') {
                return 'Pool Campus';
            }
            if (value == '3') {
                return 'Open Campus';
            }
        };
    })

    .filter('tnpNew', function () {
        return function (value) {
            if (value) {
                if (value == 'company_registration') {
                    return 'index.home.training-placement.single-companies';
                }
                else if (value == 'company_approved') {
                    return 'index.home.training-placement.single-companies';
                }
                else if (value == 'company_activated') {
                    return 'index.home.training-placement.single-companies';
                }
                else if (value == 'company_rejected') {
                    return 'index.home.training-placement.single-companies';
                }
                else if (value == 'company_updated') {
                    return 'index.home.training-placement.single-companies';
                }
                else if (value == 'consultancy_registration') {
                    return 'index.home.training-placement.single-consultancy';
                }
                else if (value == 'consultancy_updated') {
                    return 'index.home.training-placement.single-consultancy';
                }
                else if (value == 'placement_created') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
                else if (value == 'placement_rejected') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
                else if (value == 'placement_approved') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
                else if (value == 'placement_started') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
                else if (value == 'circular_updated') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
                else if (value == 'placement_deactivated') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
                else if (value == 'placement_activated') {
                    return 'index.home.training-placement.single-placement-circulars';
                }
            } else {
                return 'blank';
            }
        };
    })

    .filter('circularStatus', function () {
        return function (value) {
            if (value == '1') {
                return 'Saved';
            }
            if (value == '2') {
                return 'Approved';
            }
            if (value == '3') {
                return 'Rejected';
            }
            if (value == '4') {
                return 'Running';
            }
            if (value == '5') {
                return 'Completed';
            }
            if (value == '6') {
                return 'Deactivated';
            }
        }
    })

    .filter('circularStatusLabel', function () {
        return function (value) {
            if (value == '1') {
                return 'label-info';
            }
            if (value == '2') {
                return 'label-success';
            }
            if (value == '3') {
                return 'label-danger';
            }
            if (value == '4') {
                return 'label-warning';
            }
            if (value == '5') {
                return 'label-default';
            }
            if (value == '6') {
                return 'label-primary';
            }
        };
    })

    .filter('raiseAttendanceStatus', function () {
        return function (value) {
            if (value == '1') {
                return 'Pending';
            }
            if (value == '2') {
                return 'Approved';
            }
            if (value == '3') {
                return 'Rejected';
            }
        };
    })

    .filter('start', function () {
        return function (input, start) {
            if (!input || !input.length) {
                return;
            }

            start = +start;
            return input.slice(start);
        };
    })

    .filter('highlight', ['$sce', function ($sce) {
        return function (text, phrase) {
            if (text) {
                if (phrase) {
                    text = text.replace(new RegExp('(' + phrase + ')', 'gi'), '<span class="highlighted">$1</span>')
                }

                return $sce.trustAsHtml(text)
            }
        }
    }])
    .filter('questionsection', function () {
        return function (value) {
            if (value == '1') {
                return 'Academic';
            }
            if (value == '2') {
                return 'Career';
            }
            if (value == '3') {
                return 'Industrial';
            }
            if (value == '4') {
                return 'Other';
            }
        }
    })
    .filter('questioncategory', function () {
        return function (value) {
            if (value == '1') {
                return 'Complaint';
            }
            if (value == '2') {
                return 'Compulsory';
            }
            if (value == '3') {
                return 'Critical';
            }
            if (value == '4') {
                return 'Followup';
            }
            if (value == '5') {
                return 'Normal';
            }
            if (value == '6') {
                return 'Personal';
            }
            if (value == '7') {
                return 'Resolved';
            }
        }
    })

    .filter('boardName', function () {
        return function (value) {
            if (value == '1') {
                return 'State Board';
            }
            if (value == '2') {
                return 'CBSE';
            }
            if (value == '3') {
                return 'ICSE';
            }
            if (value == '4') {
                return 'Other Board';
            }
        };
    })

    .filter('placementAnswer', function () {
        return function (value) {
            if (value == 'yes') {
                return 'Yes';
            }
            if (value == 'no') {
                return 'No';
            }
        };
    })

    .filter('attempt', function () {
        return function (value) {
            if (value == -1) {
                return 'Not Cleared';
            }
            else {
                return value;
            }
        };
    })

    .filter('counselingStatus', function () {
        return function (value) {
            if (value == 0) {
                return 'Pending';
            }
            if (value == 1) {
                return 'Completed';
            }
            if (value == 2) {
                return 'Not Repoted';
            }
            if (value == 3) {
                return 'Saved';
            }
        };
    })

    .filter('counStatusCls', function () {
        return function (value) {
            if (value == 0) {
                return 'couns-saved';
            }
            if (value == 1) {
                return 'couns-complete';
            }
        };
    })

    .filter('lableCls', function () {
        return function (value) {
            if (value == 0) {
                return 'label-danger';
            }
            if (value == 1) {
                return 'label-default';
            }
            if (value == 2) {
                return 'label-danger';
            }
            if (value == 3) {
                return 'label-info';
            }
        };
    })
    .filter('counselingLabelCls', function () {
        return function (value) {
            if (value == 0) {
                return 'label-info';
            }
            if (value == 1) {
                return 'label-success';
            }
            if (value == 2) {
                return 'label-danger';
            }
            if (value == 3) {
                return 'label-warning';
            }
        };
    })

    .filter('campusInterest', function () {
        return function (value) {
            if (value == '1') {
                return 'Pending';
            }
            if (value == '2') {
                return 'Interested';
            }
            if (value == '3') {
                return 'Not Interested';
            }
        };
    })

    .filter('campusInterestLabel', function () {
        return function (value) {
            if (value == '1') {
                return 'label-danger';
            }
            if (value == '2') {
                return 'label-success';
            }
            if (value == '3') {
                return 'label-default';
            }
        };
    })

    .filter('extraAttndance', function () {
        return function (value) {
            if (value == '1') {
                return 'Pending at mentor';
            }
            if (value == '2') {
                return 'Pending at HOD';
            }
            if (value == '3') {
                return 'Approved';
            }
            if (value == '4') {
                return 'Rejected by mentor';
            }
            if (value == '5') {
                return 'Rejected by HOD';
            }
        }
    })

    .filter('attncolor', function () {
        return function (value) {
            if (parseFloat(value) >= 0 && parseFloat(value) <= 10) {
                return '#ff0000';
            }
            if (parseFloat(value) >= 11 && parseFloat(value) <= 40) {
                return '#ff961a';
            }
        }
    })

    .filter('busshift', function () {
        return function (value) {
            if (value == 3) {
                return 1;
            }
            else if (value == 4) {
                return 2;
            } else {
                return value;
            }
        }
    })

    .filter('clockcolor', function ($filter) {
        return function (value) {
            var startTime = $filter('amDateFormat')($filter('amFromUnix')(value), 'H');
            if (startTime <= 9) {
                return '#5284c3';
            }
            else if (startTime > 9 && startTime <= 11) {
                return '#99d2ff';
            }
            else if (startTime > 11 && startTime <= 13) {
                return '#fbbe00';
            }
            else if (startTime > 13 && startTime <= 15) {
                return '#e0ab4f';
            }
            else if (startTime > 15) {
                return '#be4e26';
            } else {
                return '#00adef';
            }
        }
    })

    .filter('achievements_type', function () {
        return function (value) {
            var val = parseInt(value);
            if (val === 1) {
                return 'Paper & Publication'
            }
            if (val === 2) {
                return 'Others';
            }
            if (val === 3) {
                return 'Technical Seminar';
            }
            if (val === 4) {
                return 'Workshop';
            }
            if (val === 5) {
                return 'Competitions';
            }
            if (val === 6) {
                return 'Sports Activities';
            }
        }
    })

    .filter('studentcategory', function () {
        return function (value) {
            var val = parseInt(value);
            if (val === 1) {
                return 'General'
            }
            else if (val === 2) {
                return 'OBC';
            }
            else if (val === 3) {
                return 'ST';
            }
            else if (val === 4) {
                return 'SC';
            }
            else {
                return '-';
            }
        }
    });




