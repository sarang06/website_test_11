angular.module('ecampus.services').factory('Service', ['$http', 'API', '$q', function ($http, API, $q) {
    var departments;
    return {
        authState: function (inputData) {
            var defer = $q.defer();
            $http.post(API.auth_state, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        login: function (loginFormData) {
            var defer = $q.defer();
            $http.post(API.user_login, loginFormData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        inviteNew: function (inputData) {
            var defer = $q.defer();
            $http.post(API.invite_new, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getUserTypes: function () {
            var defer = $q.defer();
            $http.get(API.user_types).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDepartments: function () {
            var defer = $q.defer();
            if (departments) {
                return departments;
            }
            $http.get(API.get_departments).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            departments = defer.promise;
            return departments;
        },
        addHod: function (addInputData) {
            var defer = $q.defer();
            $http.post(API.add_hod, addInputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getHods: function () {
            var defer = $q.defer();
            $http.get(API.get_hods).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addTeacher: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_teacher, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getHodTeachers: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_hod_teachers, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStudent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_student, inputData).then(function (res) {
                defer.resolve(res);
            }, function () {
                defer.reject(res);
            });
            return defer.promise;
        },
        getUserProfile: function () {
            var defer = $q.defer();
            $http.get(API.get_user_profile).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDepartmentTeacher: function () {
            var defer = $q.defer();
            $http.get(API.get_department_teachers).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDepartmentSubject: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_department_subject, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        createTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.create_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getBranches: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_branches, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getWeekDays: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_week_days, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function () {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStudent: function (inputdata) {
            var defer = $q.defer();
            $http.post(API.get_student, inputdata).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        takeAttendence: function (inputData) {
            var defer = $q.defer();
            $http.post(API.take_attendence, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_profile, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        postNewsFeed: function (inputData) {
            var defer = $q.defer();
            $http.post(API.post_news_feed, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getNewsFeed: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_news_feed, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadNewsfeedImage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_neswfeed_image, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadNewsfeedAttechedment: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_newsfeed_attechedment, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadProfilePicture: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_profile_picture, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getModerator: function () {
            var defer = $q.defer();
            $http.get(API.get_moderator).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAttendence: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_attendence, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        approvedPost: function (inputData) {
            var defer = $q.defer();
            $http.post(API.approved_posts, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        declinedPost: function (inputData) {
            var defer = $q.defer();
            $http.post(API.declined_posts, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        archivedsPost: function (inputData) {
            var defer = $q.defer();
            $http.post(API.archived_post, inputData).then(function (res) {
                defer.resolve(res);
            }, function () {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllFeed: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_feeds, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getOwnPosts: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_own_post, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addCommentsOnPost: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_comments_on_post, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getRecentPost: function () {
            var defer = $q.defer();
            $http.post(API.get_recenet_attendence).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getRecentLectureAtt: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_lecture_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSocialProfile: function () {
            var defer = $q.defer();
            $http.get(API.get_social_profile).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateSocialProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_social_profile, inputData).then(function (res) {
                defer.resolve(res);
            }, function () {
                defer.reject(res);
            });
            return defer.promise;
        },
        getEducationalProfile: function () {
            var defer = $q.defer();
            $http.get(API.get_education_pofile).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addEducationalProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_education_pofile, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateEducationalProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_education_pofile, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteEducationalProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_education_pofile, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadResultCsv: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_csv, inputData,
                {
                    headers: {
                        'Content-Type': undefined
                    }
                }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadMstResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_mst_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMstResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_mst_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMstResultMarks: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_mst_result_marks, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadSessionalResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_sessional_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSessionalResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_sessional_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSessionalResultMarks: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_sessional_result_marks, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadSemesterResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_semester_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSemesterResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_semester_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSemesterResultMark: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_semester_result_marks, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadSemesterGradeResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_semester_grade_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSemesterGradeResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_smester_grades_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSemesterGradeResultMark: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_semester_grade_result_marks, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getUsers: function () {
            var defer = $q.defer();
            $http.get(API.get_users).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        sendMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.send_message, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addMsgAttchment: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_msg_attachment, inputData,
                {
                    headers: {
                        'Content-Type': undefined
                    }
                }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getInboxMsg: function (limit, pageNo) {
            var defer = $q.defer();
            $http.get(API.get_inbox_msg + '/' + limit + '/' + pageNo).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSentMsg: function (limit, pageNo) {
            var defer = $q.defer();
            $http.get(API.get_sent_msg + '/' + limit + '/' + pageNo).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getInboxMsgDetail: function (msgId) {
            var defer = $q.defer();
            $http.get(API.get_inbox_msg_detail + '/' + msgId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        draftMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.draft_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getNotifications: function (flag) {
            var defer = $q.defer();
            $http.get(API.get_notifications + '/' + flag).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        resetNotifications: function () {
            var defer = $q.defer();
            $http.get(API.reset_notifications).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDraftMsg: function (limit, pageNo) {
            var defer = $q.defer();
            $http.get(API.get_draft_threads + '/' + limit + '/' + pageNo).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        startedMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.started_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStartedMsg: function (limit, pageNo) {
            var defer = $q.defer();
            $http.get(API.get_started_msg + '/' + limit + '/' + pageNo).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteInboxMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_inbox_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteSentMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_sent_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteDraftMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_draft_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        createLabel: function (inputData) {
            var defer = $q.defer();
            $http.post(API.create_lable, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getLabel: function () {
            var defer = $q.defer();
            $http.get(API.get_lable).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addIntoLabel: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_into_label, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDataIntoLabel: function (labelId, limit, pageNo) {
            var defer = $q.defer();
            $http.get(API.get_data_into_label + '/' + labelId + '/' + limit + '/' + pageNo).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteLableName: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_label_name, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteLableMsg: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_label_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllRoles: function () {
            var defer = $q.defer();
            $http.get(API.all_type_roles).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        applyRoles: function (inputData) {
            var defer = $q.defer();
            $http.post(API.apply_roles, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        userRoles: function () {
            var defer = $q.defer();
            $http.get(API.user_roles).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteInboxRply: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_sub_inbox_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addAccounts: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_accounts, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getBranchStudent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_branch_student, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        allDepartMentsMentor: function () {
            var defer = $q.defer();
            $http.get(API.get_all_department_mentors).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        mentorDetails: function (inputData) {
            var defer = $q.defer();
            $http.post(API.mentor_details, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addMentorType: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_mentor_type, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        assignStudent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.assign_students, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addNewLabel: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_new_label, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getHodTimetable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_hod_timetable, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadAttandanceCsv: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_attendance_csv, inputData,
                {
                    headers: {
                        'Content-Type': undefined
                    }
                }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        submitAttandanceCsv: function (inputData) {
            var defer = $q.defer();
            $http.post(API.submit_att_csv, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTeacherResquest: function () {
            var defer = $q.defer();
            $http.get(API.get_teacher_request).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        actionOnTeacherrequest: function (inputData) {
            var defer = $q.defer();
            $http.post(API.action_on_teacherRequest, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleRequestDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_teacherRequest_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        createQuestionForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.create_ques_from, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getQuestionForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_ques_form, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        createMentorQuestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.create_mentor_ques, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMentorQuestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_mentor_ques_frm, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMentee: function () {
            var defer = $q.defer();
            $http.get(API.get_mentee).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        approveMstResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.approve_mst_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMentorQuesForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_mentor_ques_frm, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFormsQuestions: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_form_ques, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        approveSemesterGradesResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.approve_semester_grades, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        approveSessionalResult: function (inputData) {
            var defer = $q.defer();
            $http.post(API.approve_sessional_result, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        submitCounsellingForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.submit_counselling_form, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addNewQuestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_new_ques, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getPreviousCounselling: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_previous_conselling, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleCounselling: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_counselling, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getOwnCounselling: function () {
            var defer = $q.defer();
            $http.get(API.get_own_counselling).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllOurUsers: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_our_user, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        singleUserPermission: function (inputData) {
            var defer = $q.defer();
            $http.post(API.single_user_permission, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        giveAccessToUser: function (inputData) {
            var defer = $q.defer();
            $http.post(API.give_access, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeAccess: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_access, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        countOfUnreadMsg: function () {
            var defer = $q.defer();
            $http.get(API.count_of_unreadMsg).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAccountType: function () {
            var defer = $q.defer();
            $http.get(API.get_account_type).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSentMsgDetail: function (msgId) {
            var defer = $q.defer();
            $http.get(API.get_sent_msg_detail + '/' + msgId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStarMsgDetail: function (msgId) {
            var defer = $q.defer();
            $http.get(API.get_star_msg_detail + '/' + msgId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDraftMsgDetail: function (msgId) {
            var defer = $q.defer();
            $http.get(API.get_draft_msg_detail + '/' + msgId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getBranchMentee: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_branch_mentee, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleMenteeCouns: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_mentee_couns, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStudentAllDetails: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_student_all_details, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteOwnPost: function (feedId) {
            var defer = $q.defer();
            $http.delete(API.delete_own_post + '/' + feedId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAccountTypes: function () {
            var defer = $q.defer();
            $http.get(API.get_user_types).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllBranchStudents: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_branch_students, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        viewUserProfileInfo: function (userId) {
            var defer = $q.defer();
            $http.get(API.view_user_profile_info + '/' + userId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        viewUserProfilePosts: function (userId, inputData) {
            var defer = $q.defer();
            $http.post(API.view_user_profile_posts + '/' + userId, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifyEducation: function (inputData) {
            var defer = $q.defer();
            $http.post(API.verify_education, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        downloadAttachment: function (fileId) {
            var defer = $q.defer();
            $http.get(API.download_attachment + '/' + fileId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addSuggetion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_suggetion, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        changePassword: function (inputData) {
            var defer = $q.defer();
            $http.post(API.change_password, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSuggetion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_suggetion, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleSuggestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_suggetion, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        setCounsellingDates: function (inputData) {
            var defer = $q.defer();
            $http.post(API.set_counselling_dates, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        setCounsellingSchedule: function (inputData) {
            var defer = $q.defer();
            $http.post(API.set_counselling_schedule, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getCounsellingDate: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_counseling_date, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAssignedMentors: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_assigned_mentors, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        viewCounsellingDuration: function (inputData) {
            var defer = $q.defer();
            $http.post(API.view_counselling_duration, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addNewCompany: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_new_company, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getCompanies: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_companies, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleCompany: function (companyId) {
            var defer = $q.defer();
            $http.get(API.get_single_comapany + '?' + 'id' + '=' + companyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        approveCompany: function (companyId) {
            var defer = $q.defer();
            $http.get(API.approve_company + '?' + 'id' + '=' + companyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        approveCompany: function (companyId) {
            var defer = $q.defer();
            $http.get(API.approve_company + '?' + 'id' + '=' + companyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        rejectCompany: function (inputData) {
            var defer = $q.defer();
            $http.post(API.reject_company, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteCompany: function (companyId) {
            var defer = $q.defer();
            $http.get(API.delete_company + '?' + 'id' + '=' + companyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addNewConsultancy: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_new_consultancy, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getConsultancies: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_consultancies, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingelConsultancy: function (consultancyId) {
            var defer = $q.defer();
            $http.get(API.get_singel_consultancy + '?' + 'id' + '=' + consultancyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStudentBasicInfo: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_Student_basic_info, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addPlacementCircular: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_placement_circular, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addEligibilityCriteria: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_eligibility_criteria, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addFeedbackForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_feedback_form, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFeedbackForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_feedback_form, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFormQuestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_form_questions, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFeedbackBatches: function () {
            var defer = $q.defer();
            $http.get(API.get_feedback_batches).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        sendFeedback: function (inputData) {
            var defer = $q.defer();
            $http.post(API.send_feedback, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFeedback: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_feedbacks, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleFeedback: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_feedback, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editFeedback: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_feedback, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFeedbackToStudent: function () {
            var defer = $q.defer();
            $http.get(API.get_feedback_to_student).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStudentFeedbackQuestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_student_feedback_question, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        giveFeedback: function (inputData) {
            var defer = $q.defer();
            $http.post(API.give_feedback, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        feedbackSelectedBatches: function (inputData) {
            var defer = $q.defer();
            $http.post(API.feedback_selected_batches, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        feedbackReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.feedback_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFeedbackDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_feedback_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addAchievement: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_achievement, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editAchievement: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_achievement, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadAchievementFile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_achievement_attachment, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAchievements: function () {
            var defer = $q.defer();
            $http.get(API.get_achievement).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addSubject: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_subject, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addSubjectFaculty: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_subject_faculty, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        changeSubjectStatus: function (inputData) {
            var defer = $q.defer();
            $http.post(API.change_subject_status, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSubjectFaculties: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_subject_faculties, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getPlacementCircularList: function (inputData) {
            var defer = $q.defer();
            $http.post(API.placement_circular_list, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        singlePlacementCircular: function (inputData) {
            var defer = $q.defer();
            $http.post(API.single_placement_circular, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTnpNews: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_tnp_news, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        changeCircularStatus: function (inputData) {
            var defer = $q.defer();
            $http.post(API.change_circular_status, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addSession: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_session, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSession: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_session, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addHoliday: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_holiday, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getHolidays: function () {
            var defer = $q.defer();
            $http.get(API.get_holidays).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        createStudentTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.create_Student_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTimeTableSessions: function () {
            var defer = $q.defer();
            $http.get(API.get_time_table_sessions).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        copyTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.copy_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSubjectLecture: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_subject_lecture, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editSubjectLecture: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_subject_lecture, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addBreak: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_break, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },

        raiseAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.raise_attendance, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllFaculties: function (inputData) {
            var defer = $q.defer();
            $http.get(API.get_all_faculties, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAttendanceRequests: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_attendance_requests, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        actionAttendanceRequest: function (inputData) {
            var defer = $q.defer();
            $http.post(API.action_attendance_request, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMasterTimetable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_master_timetable, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMentorForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_mentor_ques_form, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        assignHodDeaprtment: function (inputData) {
            var defer = $q.defer();
            $http.post(API.assign_hod_department, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeHod: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_hod, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeSession: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_session, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllTeacher: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_teacher, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getDayLecture: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_day_lecture, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        changeTimeTable: function (inputData) {
            var defer = $q.defer();
            $http.post(API.change_time_table, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editSubject: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_subject, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStudentForm: function () {
            var defer = $q.defer();
            $http.get(API.get_student_form).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFacultySubjects: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_faculty_subjects, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateCurrentEducation: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_current_education, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        assignedFaculties: function (inputData) {
            var defer = $q.defer();
            $http.post(API.assigned_faculties, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSeniorMentor: function () {
            var defer = $q.defer();
            $http.get(API.get_senior_mentor).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getJuniorMentor: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_junior_mentor, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addJuniorMentor: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_junior_mentor, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAssignJuniorMentor: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_assign_junior_mentor, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeAssignJuniorMentor: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_assign_junior_mentor, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteCounselingForms: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_counseling_forms, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteMentorshipFormsQues: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_mentorship_forms_ques, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editMentorshipForm: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_mentorship_form, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editMentorshipQuestion: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_mentorship_question, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getCounselingDuration: function () {
            var defer = $q.defer();
            $http.get(API.get_counseling_duration).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStudentBatch: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_student_batch, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getLabBatches: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_lab_batches, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getPendingAttendence: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_pending_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadPendingAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.upload_pending_attendance, inputData,
                {
                    headers: {
                        'Content-Type': undefined
                    }
                }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        searchOnMessage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.search_on_message, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        applyForForgetPassword: function (inputData) {
            var defer = $q.defer();
            $http.post(API.apply_for_forget_password, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        forgetPasswordSubmit: function (inputData) {
            var defer = $q.defer();
            $http.post(API.forget_password_submit, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllStudent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_students, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllStudentElective: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_students_elective, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        activeOrDeactiveUsers: function (inputData) {
            var defer = $q.defer();
            $http.post(API.active_or_deactive_users, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        resetAdminPassword: function (inputData) {
            var defer = $q.defer();
            $http.post(API.reset_admin_password, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateAccountInformations: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_account_informations, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        logout: function () {
            var defer = $q.defer();
            $http.get(API.logout).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getServerDate: function () {
            var defer = $q.defer();
            $http.get(API.get_server_date).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTodayLecture: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_today_lecture, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMessageGroups: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_message_groups, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        singleMessageGroup: function (inputData) {
            var defer = $q.defer();
            $http.post(API.single_message_group, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editMessageGroup: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_message_group, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addNewMessageGroup: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_new_message_group, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMemberList: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_member_list, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addNewMember: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_new_member, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        searchMember: function (inputData) {
            var defer = $q.defer();
            $http.post(API.search_member, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllUserGroups: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_all_user_groups, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editSingleLecture: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_single_lecture, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSchoolBoards: function () {
            var defer = $q.defer();
            $http.get(API.get_school_boards).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        filterEligibleStudents: function (inputData) {
            var defer = $q.defer();
            $http.post(API.filter_eligible_students, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addSemesterDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_semester_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSemesterDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_semester_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addAcademicAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_academic_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addTrainingAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_training_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAcademicAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_academic_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTrainingAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_training_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addTrainingDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_training_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getTrainingDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_training_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeGroupMember: function (inputData) {
            console.log(inputData);
            var defer = $q.defer();
            $http.post(API.remove_group_member, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        composeMessage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.compose_message, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleMessage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_message, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteMessage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_message, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        moveMessage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.move_message, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        moveIntoInbox: function (inputData) {
            var defer = $q.defer();
            $http.post(API.move_into_inbox, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editConsultancy: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_consultancy, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editCircular: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_circular, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editCircularEligibility: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_circular_eligibility, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editCompany: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_company, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAccountGroups: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_account_groups, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        createDefaultGroup: function (inputData) {
            var defer = $q.defer();
            $http.post(API.create_default_group, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getCircularEligibility: function (companyId) {
            var defer = $q.defer();
            $http.get(API.get_circular_eligibility + '?' + 'id' + '=' + companyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        activateConsultancy: function (consultancyId) {
            var defer = $q.defer();
            $http.get(API.activate_consultancy + '?' + 'id' + '=' + consultancyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteConsultancy: function (consultancyId) {
            var defer = $q.defer();
            $http.get(API.delete_consultancy + '?' + 'id' + '=' + consultancyId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifySemesterDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.verify_semester_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifyAcademicAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.verify_academic_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifyTrainingAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.verify_training_attendance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFollowUps: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_follow_ups, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addPlacementDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_placement_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getPlacementDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_placement_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addJobProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_job_profile, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getJobProfile: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_job_profile, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeTrainingDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_training_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifyTrainingDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.verify_training_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifyPlacementDetail: function (inputData) {
            var defer = $q.defer();
            $http.post(API.verify_placement_detail, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addcommentFollowups: function (inputData) {
            var defer = $q.defer();
            $http.post(API.addcomment_followups, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        generateFeedback: function (inputData) {
            var defer = $q.defer();
            $http.get(API.generate_feedback_reports + '?id=' + inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        singleFacultyFeedback: function (inputData) {
            var defer = $q.defer();
            $http.post(API.single_faculty_feedback, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMyFeedbackReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_my_feedback, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getInterviewRounds: function (circularId) {
            var defer = $q.defer();
            $http.get(API.get_interview_rounds + '?' + 'id' + '=' + circularId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getCampusDayList: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_campus_day_list, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateCampusDayDetails: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_campus_day_details, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        closeCampus: function (circularId) {
            var defer = $q.defer();
            $http.get(API.close_campus + '?' + 'id' + '=' + circularId).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getPlacementReports: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_placement_reports, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeMentee: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_mentee, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getFacultySubject: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_faculty_subject, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editLabelName: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_label_name, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStudentEducation: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_student_education, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteStudentEducation: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_student_education, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        sendCampusNews: function (inputData) {
            var defer = $q.defer();
            $http.post(API.send_campus_news, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        checkEligibility: function () {
            var defer = $q.defer();
            $http.get(API.check_eligibility).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        submitInterest: function (inputData) {
            var defer = $q.defer();
            $http.post(API.submit_interest, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getCompanyDriveReports: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_company_drive_reports, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        exportGrievanceCSV: function (inputData) {
            var defer = $q.defer();
            $http.post(API.export_grievance_csv, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getBranchBatchReports: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_branch_batch_reports, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getPlacedStudentReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_placed_student_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getIndividualReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_individual_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        sendMessageToCandidates: function (inputData) {
            var defer = $q.defer();
            $http.post(API.send_message_to_candidates, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getBranchwiseIndividualReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_branchwise_individual_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        checkSelection: function () {
            var defer = $q.defer();
            $http.get(API.check_selection).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        submitJoiningConfirmation: function (inputData) {
            var defer = $q.defer();
            $http.post(API.submit_joining_confirmation, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        previousConselingDates: function () {
            var defer = $q.defer();
            $http.get(API.previous_conseling_dates).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getMentorsReportList: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_mentor_report_list, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleMentorReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_mentor_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getListOfEligibleStudents: function (inputData) {
            var defer = $q.defer();
            $http.post(API.list_of_eligible_stuidents, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStudentInCampus: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_student_in_campus, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        ativateOrDeactiveCampus: function (inputData) {
            var defer = $q.defer();
            $http.post(API.ativate_deactive_campus, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        sendMsgToEligibleStu: function (inputData) {
            var defer = $q.defer();
            $http.post(API.send_msg_to_eligible_stu, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        studentFeesList: function () {
            var defer = $q.defer();
            $http.get(API.student_fees_list).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getLibraryUrl: function () {
            var defer = $q.defer();
            $http.get(API.get_library_url).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        composeCircularPost: function (inputData) {
            var defer = $q.defer();
            $http.post(API.compose_circular_post, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeEligibleStudent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.remove_eligible_student, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        facultySubjectReport: function () {
            var defer = $q.defer();
            $http.get(API.faculty_subject_report).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        singleSubjectReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.single_subject_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleMentorCsv: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_mentor_csv, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        pastUsername: function (inputData) {
            var defer = $q.defer();
            $http.post(API.past_username, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        setStudentPendingAttendance: function (data) {
            console.log(data);
            var defer = $q.defer();
            $http.post(API.set_student_pending_attendance, data).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        uploadHodAttendance: function (data) {
            console.log(data);
            var defer = $q.defer();
            $http.post(API.upload_hod_attendance, data).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        placedStudentList: function (inputData) {
            var defer = $q.defer();
            $http.post(API.placed_student_list, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        downloadPlacementReport: function (inputData) {
            var defer = $q.defer();
            $http.post(API.download_placement_report, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getYourEnrollment: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_your_enrollment, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSmsContent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_sms_contents, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editSmsContent: function (inputData) {
            var defer = $q.defer();
            $http.post(API.edit_sms_content, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAttendanceReason: function () {
            var defer = $q.defer();
            $http.get(API.get_attendance_reason).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getExtraAttList: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_extra_att_list, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateExtraAttRecord: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_extra_att_record, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        raiseRangeAttendance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.raise_attendance, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSessionStudentsAtt: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_session_students_att, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        sendSmsToParents: function (inputData) {
            var defer = $q.defer();
            $http.post(API.send_sms_to_parents, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllBuses: function () {
            var defer = $q.defer();
            $http.get(API.get_all_buses).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSingleBusRoute: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_single_bus_route, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        submitBusDetails: function (inputData) {
            var defer = $q.defer();
            $http.post(API.submit_bus_details, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        myBusRoute: function () {
            var defer = $q.defer();
            $http.get(API.my_bus_route).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        mentorSelectBusRoute: function (inputData) {
            var defer = $q.defer();
            $http.post(API.mentor_select_bus_route, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        menteeBusRoute: function (inputData) {
            var defer = $q.defer();
            $http.post(API.mentee_bus_route, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        departmentTimeTableSessions: function () {
            var defer = $q.defer();
            $http.get(API.department_time_table_sessions).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAttendanceSmsReport: function (input) {
            var defer = $q.defer();
            $http.post(API.get_attendance_sms_report, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addRouteToBus: function (input) {
            var defer = $q.defer();
            $http.post(API.add_route_to_bus, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeBusRoot: function (input) {
            var defer = $q.defer();
            $http.post(API.remove_bus_root, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateBusDetails: function (input) {
            var defer = $q.defer();
            $http.post(API.update_bus_details, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllUserBus: function (input) {
            var defer = $q.defer();
            $http.post(API.get_all_user_bus, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        generateCsvInternal: function (input) {
            var defer = $q.defer();
            $http.post(API.generate_csv_internal, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAllStops: function (input) {
            var defer = $q.defer();
            $http.post(API.get_all_stops, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStop: function (input) {
            var defer = $q.defer();
            $http.post(API.add_stop, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        removeStop: function (input) {
            var defer = $q.defer();
            $http.post(API.remove_stop, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateSiteNotice: function (input) {
            var defer = $q.defer();
            $http.post(API.update_site_notice, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getSiteNotice: function () {
            var defer = $q.defer();
            $http.get(API.get_site_notice).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addAttendanceComment: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_attendance_comment, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        deleteAttendanceComment: function (inputData) {
            var defer = $q.defer();
            $http.post(API.delete_attendance_comment, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getAttendanceComments: function () {
            var defer = $q.defer();
            $http.get(API.get_attendance_comments).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        moveUserGroup: function (input) {
            var defer = $q.defer();
            $http.post(API.move_user_group, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editRouteToBus: function (input) {
            var defer = $q.defer();
            $http.post(API.edit_route_to_bus, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateElectiveSubject: function (input) {
            var defer = $q.defer();
            $http.post(API.update_elective_subject, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStudentAchievements: function (input) {
            var defer = $q.defer();
            $http.post(API.get_student_achievements, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        addStudentAchievement: function (input) {
            var defer = $q.defer();
            $http.post(API.add_student_achievement, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        verifyStudentAchievement: function (input) {
            var defer = $q.defer();
            $http.post(API.verify_student_achievement, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        editStudentAchievement: function (input) {
            var defer = $q.defer();
            $http.post(API.edit_student_achievement, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getStudentMSTResults: function (input) {
            var defer = $q.defer();
            $http.post(API.get_student_mst_result, input).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        downloadAttendanceCSV: function (a, b, c) {
            var defer = $q.defer();
            $http.get(API.get_attendance_csv + '/' + a + '/' + b + '/' + c).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        markStudentInterested: function (inputData) {
            var defer = $q.defer();
            $http.post(API.mark_student_interested, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },

        getGrievanceCategory: function () {
            var defer = $q.defer();
            $http.get(API.get_grievance_category).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getGrievanceByUser: function () {
            var defer = $q.defer();
            $http.get(API.get_grievance_by_user).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getGrievance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_grievance, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },


        addGrievance: function (inputData) {
            var defer = $q.defer();
            $http.post(API.add_grievance, inputData, {
                transformRequest: angular.identity,
                headers: {
                    'Content-Type': undefined
                }
            }).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        updateGrievanceStatus: function (inputData) {
            var defer = $q.defer();
            $http.post(API.update_grievance, inputData
            ).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        getUnapprovedPost: function (inputData) {
            var defer = $q.defer();
            $http.post(API.get_unapproved_post, inputData
            ).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        postActionAdmin: function (inputData) {
            var defer = $q.defer();
            $http.post(API.post_action_admin, inputData
            ).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        postDeleteAdmin: function (inputData) {
            var defer = $q.defer();
            $http.post(API.post_delete_admin, inputData
            ).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        viewChildProfileInfo: function () {
            var defer = $q.defer();
            $http.get(API.view_child_profile_info).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        viewChildProfilePosts: function (inputData) {
            var defer = $q.defer();
            $http.post(API.view_child_profile_posts, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        },
        backUpMessage: function (inputData) {
            var defer = $q.defer();
            $http.post(API.back_up_msg, inputData).then(function (res) {
                defer.resolve(res);
            }, function (res) {
                defer.reject(res);
            });
            return defer.promise;
        }
    };
}]);
