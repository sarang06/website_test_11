angular.module('ecampus').controller('messageController', ['$scope', 'Service', '$state', '$rootScope', 'API', 'Storage', '$timeout', function ($scope, Service, $state, $rootScope, API, Storage, $timeout) {

    $scope.paste = function () {
        setTimeout(function () {
            document.getElementById('members_value').addEventListener('paste', function (evt) {
                var pasteContent = evt.clipboardData.getData('text/plain');
                evt.preventDefault();
                pasteContent = pasteContent.replace('\n', ' ').split(' ');
                Service.pastUsername({'content': pasteContent}).then(function (res) {
                    angular.forEach(res.data.response, function (val, key) {
                        var user = {'originalObject': val};
                        $scope.selectedUser(user);
                    });
                }, function (res) {
                });
            });
        }, 1000);

        $scope.ReceiverIdArray = [];
        $scope.composeMessageObj = {
            image: [], receiverId: [], attachment: []
        };
        $scope.msgLoadingImg = {
            data: []
        };
        $scope.msgLoadingAttechment = {
            data: []
        };
        $scope.signature();
    };

    $scope.initMessageAction = function () {
        $scope.ReceiverIdArray = [];
        $scope.composeMessageObj = {
            image: [], receiverId: [], attachment: []
        };
        $scope.msgLoadingImg = {
            data: []
        };
        $scope.msgLoadingAttechment = {
            data: []
        };
    };

    $scope.ReceiverIdArray = [];
    $scope.composeMessageObj = {
        image: [], receiverId: [], attachment: []
    };
    $scope.msgLoadingImg = {
        data: []
    };
    $scope.msgLoadingAttechment = {
        data: []
    };

    $scope.moveToInboxObj = {};
    $scope.moveMessageObj = {};
    $scope.deleteMessagesObj = {};
    $scope.deleteSentMessageObj = {};
    $scope.deleteStarMessageObj = {};
    $scope.deleteInboxMessageObj = {};
    $scope.deleteDraftMessageObj = {};
    $scope.deleteLableMessageObj = {};
    $scope.deleteSearchMessageObj = {};
    $scope.moveMessageObj.thread_id = [];
    $scope.moveToInboxObj.thread_id = [];
    $scope.deleteMessagesObj.thread_id = [];

    $scope.getUserProfiles = function () {
        Service.getUserProfile().then(function (res) {
            $scope.userProfileData = res.data.response;
        }, function (res) {
        });
    };

    $timeout(function () {
        var searchInput;
        if (document.getElementById('members_value')) {
            searchInput = document.getElementById('members_value');
            searchInput.focus();
        }
        if (document.getElementById('forward_value')) {
            searchInput = document.getElementById('forward_value');
            searchInput.focus();
        }
        if (document.getElementById('message')) {
            searchInput = document.getElementById('message');
            searchInput.focus();
        }
    }, 500);

    $scope.limit = '10';

    $scope.getUser = API.get_users;
    $scope.getUserData = [];
    $scope.getUserList = function () {
        Service.getUsers().then(function (res) {
            $scope.getUserData = res.data.response;
        }, function (res) {
            $scope.getUserData = [];
        })
    };

    $(window).on("beforeunload", function () {
        return;
    });

    //----------------------------------------------------sent-message---------------------------------------------------//

    $scope.selectedUser = function (user) {
        $scope.forwardReceiver = user.originalObject;
        $scope.ReceiverIdArray.push(user.originalObject);
        $timeout(function () {
            var searchInput;
            if (document.getElementById('members_value')) {
                searchInput = document.getElementById('members_value');
            } else if (document.getElementById('forward_value')) {
                searchInput = document.getElementById('forward_value');
            }
            searchInput.focus();
        }, 500);
    };

    $scope.removeSelectedUser = function (index) {
        $scope.ReceiverIdArray.splice(index, 1);
    };

    $scope.attechmesentRplyOfMessagentData = [];
    var uploadMsgXhr = new XMLHttpRequest();
    var measure = {};
    $scope.addMsgAttechments = function () {
        var fd = new FormData();
        var file = $scope.uploadFile;
        if (file.size > $rootScope.maxAttachmentSize) {
            $.alert('Max file size 10 MB');
            return;
        }
        fd.append('attachment', file);
        $scope.sendMessageData.disabled = true;
        $scope.msgLoadingAttechment.show = true;

        uploadMsgXhr.upload.onprogress = function (e) {
            $scope.$apply(function () {
                if (e.lengthComputable) {
                    $scope.msgLoadingAttechment.per = Math.round(e.loaded / e.total * 100);
                    $scope.msgLoadingAttechment.text = $scope.msgLoadingAttechment.per + '%';
                    if ($scope.msgLoadingAttechment.per >= 100) {
                        $scope.msgLoadingAttechment.show = false;
                    }
                }
            });
        };

        uploadMsgXhr.upload.onload = function (e) {
            $scope.$apply(function () {
                uploadMsgXhr.onreadystatechange = function () {
                    if (uploadMsgXhr.readyState === 4) {
                        var response;
                        if (uploadMsgXhr.status === 200) {
                            $scope.sendMessageData.disabled = false;
                            response = JSON.parse(uploadMsgXhr.responseText);
                            $scope.msgLoadingAttechment.data.push(response.response);
                            $scope.$apply();
                        } else if (uploadMsgXhr.status === 400) {
                            $scope.sendMessageData.disabled = false;
                            response = JSON.parse(uploadMsgXhr.responseText);
                            $.alert(response.message);
                            $scope.$apply();
                        }
                    }
                }
            });
        };

        uploadMsgXhr.open('POST', $rootScope.base_url + '/api/add-attachment', true);
        uploadMsgXhr.setRequestHeader('Authorization', 'Bearer ' + Storage.get("ecampus_auth", true).token);
        uploadMsgXhr.send(fd);
    };

    $scope.addMsgImages = function () {
        var fd = new FormData();
        var file = $scope.uploadFile;
        if (file.size > $rootScope.maxAttachmentSize) {
            $.alert('Max image size 10 MB');
            return false;
        }
        fd.append('image', file);
        $scope.msgLoadingImg.show = true;
        $scope.sendMessageData.disabled = true;
        uploadMsgXhr.upload.onprogress = function (e) {
            $scope.$apply(function () {
                if (e.lengthComputable) {
                    $scope.msgLoadingImg.per = Math.round(e.loaded / e.total * 100);
                    $scope.msgLoadingImg.text = $scope.msgLoadingImg.per + '%';
                    if ($scope.msgLoadingImg.per >= 100) {
                        $scope.msgLoadingImg.show = false;
                    }
                }
            });
        };

        uploadMsgXhr.upload.onload = function (e) {
            $scope.$apply(function () {
                uploadMsgXhr.onreadystatechange = function () {
                    if (uploadMsgXhr.readyState === 4) {
                        var response;
                        if (uploadMsgXhr.status === 200) {
                            $scope.sendMessageData.disabled = false;
                            response = JSON.parse(uploadMsgXhr.responseText)
                            $scope.msgLoadingImg.data.push(response.response);
                            $scope.$apply();
                        } else if (uploadMsgXhr.status === 400) {
                            $scope.sendMessageData.disabled = false;
                            response = JSON.parse(uploadMsgXhr.responseText);
                            $.alert(response.message);
                            $scope.$apply();
                        }
                    }

                }
            });
        };

        uploadMsgXhr.open('POST', $rootScope.base_url + '/api/add-attachment', true);
        uploadMsgXhr.setRequestHeader('Authorization', 'Bearer ' + Storage.get("ecampus_auth", true).token);
        uploadMsgXhr.send(fd);
    };

    $scope.abortMsgImg = function () {
        uploadMsgXhr.abort();
        $scope.msgLoadingImg.show = false;
        $scope.msgLoadingAttechment.show = false;
        $scope.sendMessageData.disabled = false;
    };

    $scope.attArray = [];
    $scope.getAttechement = function () {
        $scope.attArray.push($scope.attechmentData);
    };

    $scope.removeAttechment = function (index) {
        $scope.msgLoadingAttechment.data.splice(index, 1);
    };

    $scope.imgArray = [];
    $scope.getImage = function () {
        $scope.imgArray.push($scope.imageData);
    };

    $scope.removeImage = function (index) {
        $scope.msgLoadingImg.data.splice(index, 1);
    };

    $scope.sendMessageData = {};
    $scope.receiverId = [];
    $scope.sendMessageData.parent_msgId = 0;
    $scope.sendMessageData.msgId = "";
    $scope.sendMessageData.smsStatus = 0;
    $scope.sendMessageData.smsAlertStatus = 0;
    $scope.sendMessageData.emailAlertStatus = 0;
    $scope.sendMessageData.image = [];
    $scope.sendMessageData.attachment = [];

    $scope.getSentData = [];
    $scope.sentPagination = {};
    $scope.sentPagination.limit = '' + 10 + '';
    $scope.sentPagination.pageNo = 1;
    $scope.sentStartNo = (parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)) + 1;
    $scope.sentEndNo = parseInt($scope.pagination.limit) * ($scope.pagination.pageNo);
    $scope.getSentMsgs = function () {
        if ($scope.sentPagination.disabled) {
            return false;
        }
        $scope.loadingMessage = true;
        $scope.deleteSentMessageObj.thread_id = [];
        $scope.deleteStarMessageObj.thread_id = [];
        $scope.deleteDraftMessageObj.thread_id = [];
        $scope.deleteInboxMessageObj.thread_id = [];
        $scope.messageSearch = false;
        $scope.sentPagination.disabled = true;
        Service.getSentMsg($scope.sentPagination.limit, parseInt($scope.sentPagination.limit) * ($scope.sentPagination.pageNo - 1)).then(function (res) {
            $scope.getSentData = res.data.response;
            $scope.sentCount = res.data.total;
            $scope.sentPagination.maxPage = Math.ceil($scope.sentCount / $scope.sentPagination.limit);

            $scope.sentStartNo = (parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)) + 1;
            $scope.sentEndNo = parseInt($scope.pagination.limit) * ($scope.pagination.pageNo);

            $scope.sentPagination.disabled = false;
            $scope.loadingMessage = false;
        }, function (res) {
            $scope.noSentData = res.data.response;
            $scope.getSentData = [];
            $scope.sentPagination.disabled = false;
            $scope.loadingMessage = false;
        })
    };

    $scope.sentBackward = function () {
        if ($scope.sentPagination.disabled) {
            return false;
        }
        if ($scope.sentPagination.pageNo > 1) {
            $scope.sentPagination.disabled = true;
            Service.getSentMsg($scope.sentPagination.limit, parseInt($scope.sentPagination.limit) * ($scope.sentPagination.pageNo - 2)).then(function (res) {
                $scope.getSentData = res.data.response;

                $scope.sentPagination.pageNo = $scope.sentPagination.pageNo - 1;
                $scope.sentStartNo = (parseInt($scope.sentPagination.limit) * ($scope.sentPagination.pageNo - 1)) + 1;
                $scope.sentEndNo = parseInt($scope.sentPagination.limit) * ($scope.sentPagination.pageNo);

                $scope.sentPagination.disabled = false;
            }, function (res) {
                $scope.noSentData = res.data.response;
                $scope.getSentData = [];
                $scope.sentPagination.disabled = false;
            });
        }
    };

    $scope.sentForward = function () {
        if ($scope.sentPagination.disabled) {
            return false;
        }
        if ($scope.sentPagination.pageNo < $scope.sentPagination.maxPage) {
            $scope.sentPagination.disabled = true;
            Service.getSentMsg($scope.sentPagination.limit, parseInt($scope.sentPagination.limit) * $scope.sentPagination.pageNo).then(function (res) {
                $scope.getSentData = res.data.response;

                $scope.sentPagination.pageNo = $scope.sentPagination.pageNo + 1;
                $scope.sentStartNo = (parseInt($scope.sentPagination.limit) * ($scope.sentPagination.pageNo - 1)) + 1;
                $scope.sentEndNo = parseInt($scope.sentPagination.limit) * ($scope.sentPagination.pageNo);

                $scope.sentPagination.disabled = false;
            }, function (res) {
                $scope.noSentData = res.data.response;
                $scope.getSentData = [];
                $scope.sentPagination.disabled = false;
            });
        }
    };

    $scope.confirmForSentbox = function () {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see message!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteSentMsg();
        });
    };

    $scope.deleteSentData = {};
    $scope.deleteSentData.msgId = [];
    $scope.deleteSentMsg = function () {
        $scope.deleteSentData.disabled = true;
        Service.deleteSentMsg($scope.deleteSentData).then(function (res) {
            swal('Success', res.data.response, 'success');
            $scope.getSentMsgs();
            $scope.getStartedMsgs();
        }, function (res) {
        });
    };

    $scope.selectAllSentMsg = function () {
        $scope.deleteSentData.msgId = [];
        $("input[type='checkbox'][name='delete-msg']").prop('checked', true);
        for (var i = 0; i < $scope.getSentData.length; i++) {
            $scope.deleteSentData.msgId.push($scope.getSentData[i].msgId);
        }
        if ($scope.deleteSentData.msgId) {
            $scope.allSent = true;
        }
    };

    $scope.deselectAllSentMsg = function () {
        $scope.deleteSentData.msgId = [];
        $("input[type='checkbox'][name='delete-msg']").prop('checked', false);
        for (var i = 0; i < $scope.getSentData.length; i++) {
            if (getSentData[i].msgId) {
                $scope.deleteSentData.msgId.splice($scope.getSentData[i].msgId);
            }
        }
        $scope.allSent = false;
    };

    $scope.addLableData = {};
    $scope.addSentMsgIntoLabel = function (labelId) {
        $scope.addLableData.labelId = labelId;
        Service.addIntoLabel($scope.addLableData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $state.reload();
            }, function () {
            });
        }, function (res) {
        });
    };


    //----------------------------------------------------sent-message---------------------------------------------------//

    //----------------------------------------------------inbox---------------------------------------------------//
    $scope.getInboxData = [];
    $scope.pagination = {};
    $scope.pagination.limit = '' + 10 + '';
    $scope.pagination.pageNo = 1;
    $scope.pagination.offset = 0;
    $scope.startNo = (parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)) + 1;
    $scope.endNo = parseInt($scope.pagination.limit) * ($scope.pagination.pageNo);
    $scope.getInboxMsgs = function () {
        if ($scope.pagination.disabled) {
            return false;
        }
        $scope.loadingMessage = true;
        $scope.deleteSentMessageObj.thread_id = [];
        $scope.deleteStarMessageObj.thread_id = [];
        $scope.deleteDraftMessageObj.thread_id = [];
        $scope.deleteInboxMessageObj.thread_id = [];
        $scope.messageSearch = false;
        $scope.pagination.disabled = true;
        Service.getInboxMsg($scope.pagination.limit, parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)).then(function (res) {
            $scope.loadingMessage = false;
            $scope.getInboxData = res.data.response;
            $scope.getCountOfUnreadMsg();
            $scope.inboxCount = res.data.total;
            $scope.pagination.maxPage = Math.ceil($scope.inboxCount / $scope.pagination.limit);
            $scope.startNo = (parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)) + 1;
            $scope.endNo = parseInt($scope.pagination.limit) * ($scope.pagination.pageNo);
            $scope.SenderUserId = Storage.get('ecampus_auth', true).id;
            $scope.pagination.disabled = false;
        }, function (res) {
            $scope.loadingMessage = false;
            $scope.noInboxData = res.data.response;
            $scope.getInboxData = [];
            $scope.pagination.disabled = false;
        })
    };

    $scope.backward = function () {
        if ($scope.pagination.disabled) {
            return false;
        }
        if ($scope.pagination.pageNo > 1) {
            $scope.pagination.disabled = true;
            Service.getInboxMsg($scope.pagination.limit, parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 2)).then(function (res) {
                $scope.getInboxData = res.data.response;
                $scope.inboxCount = res.data.total;
                $scope.pagination.pageNo = $scope.pagination.pageNo - 1;
                $scope.startNo = (parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)) + 1;
                $scope.endNo = parseInt($scope.pagination.limit) * ($scope.pagination.pageNo);

                $scope.pagination.disabled = false;
            }, function (res) {
                $scope.noInboxData = res.data.response;
                $scope.getInboxData = [];
                $scope.pagination.disabled = false;
            });
        }
    };

    $scope.forward = function () {
        if ($scope.pagination.disabled) {
            return false;
        }
        if ($scope.pagination.pageNo < $scope.pagination.maxPage) {
            $scope.pagination.disabled = true;
            Service.getInboxMsg($scope.pagination.limit, parseInt($scope.pagination.limit) * $scope.pagination.pageNo).then(function (res) {
                $scope.getInboxData = res.data.response;
                $scope.pagination.pageNo = $scope.pagination.pageNo + 1;
                $scope.startNo = (parseInt($scope.pagination.limit) * ($scope.pagination.pageNo - 1)) + 1;
                $scope.endNo = parseInt($scope.pagination.limit) * ($scope.pagination.pageNo);
                $scope.pagination.disabled = false;
            }, function (res) {
                $scope.noInboxData = res.data.response;
                $scope.getInboxData = [];
                $scope.pagination.disabled = false;
            });

        }
    };

    $scope.getInboxMsgData = [];
    $scope.getInboxMsgDetail = function () {
        $scope.reply = false;
        $scope.getInboxMsgData = [];
        $scope.messageSearch = false;
        Service.getInboxMsgDetail($state.params.msgId).then(function (res) {
            $scope.getInboxMsgData = res.data.response;
            $rootScope.InboxSubject = $scope.getInboxMsgData.subject;
            $scope.userId = Storage.get('ecampus_auth', true).id;
            $scope.getCountOfUnreadMsg();
        }, function (res) {
            $scope.getInboxMsgData = [];
        })
    };

    $scope.confirmForInbox = function () {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see message!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteInboxMsg();
        });
    };

    $scope.deleteInBoxData = {};
    $scope.deleteInBoxData.msgResId = [];
    $scope.deleteInboxMsg = function () {
        Service.deleteInboxMsg($scope.deleteInBoxData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $scope.getInboxMsgs();
            }, function () {
            });
        }, function (res) {
        });
    };

    $scope.selectAllInboxMsg = function () {
        $scope.deleteInBoxData.msgResId = [];
        $("input[type='checkbox'][name='delete-inbox-msg']").prop('checked', true);
        for (var i = 0; i < $scope.getInboxData.length; i++) {
            $scope.deleteInBoxData.msgResId.push($scope.getInboxData[i].msgResId);
            $scope.msgId.push($("input[name=delete-inbox-msg]:checked").attr('msg'));
        }
        if ($scope.deleteInBoxData.msgResId) {
            $scope.allInbox = true;
        }
    };

    $scope.deselectAllInboxMsg = function () {
        $scope.deleteInBoxData.msgResId = [];
        $("input[type='checkbox'][name='delete-inbox-msg']").prop('checked', false);
        for (var i = 0; i < $scope.getInboxData.length; i++) {
            $scope.deleteInBoxData.msgResId.splice($scope.getInboxData[i].msgResId);
            $scope.msgId.splice($("input[name=delete-inbox-msg]:checked").attr('msg'));
        }
        $scope.allInbox = false;
    };

    $scope.addLableData.msgId = [];
    $scope.addInboxMsgIntoLabel = function (labelId) {
        $scope.addLableData.labelId = labelId;
        Service.addIntoLabel($scope.addLableData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $state.reload();
            }, function () {
            });
        }, function (res) {
        });
    };

    $scope.getDraftData = [];
    $scope.draftPagination = {};
    $scope.draftPagination.limit = 10;
    $scope.draftPagination.pageNo = 0;
    $scope.draftStartNo = (10 * (($scope.draftPagination.pageNo + 1) - 1)) + ($scope.draftPagination.pageNo + 1);
    $scope.darftEndNo = (10 * ($scope.draftPagination.pageNo + 1));
    $scope.getDraftMsgs = function (limit) {
        $scope.loadingMessage = true;
        $scope.deleteSentMessageObj.thread_id = [];
        $scope.deleteStarMessageObj.thread_id = [];
        $scope.deleteDraftMessageObj.thread_id = [];
        $scope.deleteInboxMessageObj.thread_id = [];
        if (limit) {
            $scope.draftPagination.limit = limit;
            $scope.draftStartNo = ($scope.draftPagination.limit * (($scope.draftPagination.pageNo + 1) - 1)) + ($scope.draftPagination.pageNo + 1);
            $scope.darftEndNo = ($scope.draftPagination.limit0 * ($scope.draftPagination.pageNo + 1));
        }
        $scope.messageSearch = false;
        Service.getDraftMsg($scope.draftPagination.limit, $scope.draftPagination.pageNo).then(function (res) {
            $scope.getDraftData = res.data.response;
            $scope.draftCount = res.data.total;
            $scope.draftPagination.maxPage = Math.ceil($scope.draftCount / $scope.draftPagination.limit);
            $scope.loadingMessage = false;
        }, function (res) {
            $scope.noDraftData = res.data.response;
            $scope.getDraftData = [];
            $scope.loadingMessage = false;
        })
    };

    $scope.darftBackward = function () {
        if ($scope.draftPagination.pageNo != 0) {
            if ($scope.draftPagination.pageNo == $scope.draftPagination.limit) {
                $scope.draftPagination.pageNo = $scope.draftPagination.pageNo - $scope.draftPagination.limit;
            } else {
                $scope.draftPagination.pageNo = ($scope.draftPagination.pageNo * $scope.draftPagination.limit) - $scope.draftPagination.limit;
            }
            Service.getDraftMsg($scope.draftPagination.limit, $scope.draftPagination.pageNo).then(function (res) {
                $scope.getDraftData = res.data.response;
                $scope.inboxCount = res.data.total;
            }, function (res) {
                $scope.noDraftData = res.data.response;
                $scope.getDraftData = [];
            });
        }
        $scope.draftStartNo = $scope.draftPagination.pageNo + 1;
        $scope.darftEndNo = $scope.draftPagination.limit;
    };

    $scope.draftForward = function () {
        if (($scope.draftPagination.pageNo + 1) < $scope.draftPagination.maxPage) {
            $scope.draftPagination.pageNo = $scope.draftPagination.pageNo + 1;
            Service.getDraftMsg($scope.draftPagination.limit, $scope.draftPagination.pageNo * $scope.draftPagination.limit).then(function (res) {
                $scope.getDraftData = res.data.response;
            }, function (res) {
                $scope.noDraftData = res.data.response;
                $scope.getDraftData = [];
            });
            $scope.draftStartNo = ($scope.draftPagination.limit * $scope.draftPagination.pageNo) + 1;
            $scope.darftEndNo = ($scope.draftPagination.limit * ($scope.draftPagination.pageNo + 1));
        }
    };

    $scope.confirmForDraft = function () {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see message!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteDraftMsg();
        });
    };

    $scope.deleteDraftData = {};
    $scope.deleteDraftData.msgId = [];
    $scope.deleteDraftMsg = function () {
        Service.deleteDraftMsg($scope.deleteDraftData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $scope.getDraftMsgs();
            }, function () {
            });
        }, function (res) {
        });
    };

    $scope.selectAllDraftMsg = function () {
        $scope.deleteDraftData.msgId = [];
        $("input[type='checkbox'][name='delete-draft-msg']").prop('checked', true);
        for (var i = 0; i < $scope.getDraftData.length; i++) {
            $scope.deleteDraftData.msgId.push($scope.getDraftData[i].msgId);
        }
        if ($scope.deleteDraftData.msgId) {
            $scope.allDraft = true;
        }
    };

    $scope.deselectAllDraftMsg = function () {
        $scope.deleteDraftData.msgId = [];
        $("input[type='checkbox'][name='delete-draft-msg']").prop('checked', false);
        for (var i = 0; i < $scope.getDraftData.length; i++) {
            $scope.deleteDraftData.msgId.splice($scope.getDraftData[i].msgId);
        }
        $scope.allDraft = false;
    };

    $scope.addDraftMsgIntoLabel = function (labelId) {
        $scope.addLableData.labelId = labelId;
        $scope.addLableData.msgId = $scope.deleteDraftData.msgId;
        Service.addIntoLabel($scope.addLableData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $state.reload();
            }, function () {
            });
        }, function (res) {
        });
    };

    $scope.getDraftMsgDetail = function () {
        Service.getDraftMsgDetail($state.params.msgId).then(function (res) {
            $scope.geDraftMsgData = res.data.response;
            $rootScope.draftSubject = $scope.geDraftMsgData.subject;
            for (i = 0; i < $scope.geDraftMsgData.receiverData.length; i++) {
                $scope.ReceiverIdArray.push($scope.geDraftMsgData.receiverData[i]);
            }
            for (j = 0; j < $scope.geDraftMsgData.attachement.length; j++) {
                if ($scope.geDraftMsgData.attachement[j].image == 1) {
                    $scope.geDraftMsgData.image.push($scope.geDraftMsgData.attachement[j].attachment);
                }
                if ($scope.geDraftMsgData.attachement[j].image == 0) {
                    $scope.geDraftMsgData.attachment.push($scope.geDraftMsgData.attachement[j].attachment);
                }
            }
        }, function (res) {
        })
    };

    $scope.sendMessageFormDraft = function () {
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            $scope.receiverId.push($scope.ReceiverIdArray[i].receiverId);
        }
        angular.forEach($scope.msgLoadingImg.data, function (val, key) {
            $scope.geDraftMsgData.image.push(val);
        });
        angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
            $scope.geDraftMsgData.attachment.push(val);
        });
        $scope.geDraftMsgData.receiverId = $scope.receiverId
        if (!$scope.geDraftMsgData.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.geDraftMsgData.msg && !$scope.geDraftMsgData.image[0] && !$scope.geDraftMsgData.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.geDraftMsgData.disabled) {
                return false;
            }
            $scope.geDraftMsgData.disabled = true;
            Service.sendMsg($scope.geDraftMsgData).then(function (res) {
                $scope.geDraftMsgData.disabled = false;
                swal('Success', res.data.response, 'success').then(function () {
                    $state.reload();
                }, function () {
                });
            }, function (res) {
                $scope.geDraftMsgData.disabled = false;
                swal('Error', res.data.response, 'error');
            });
        }
    };

    $scope.romeveDraftAtt = function (index) {
        $scope.geDraftMsgData.attachement.splice(index, 1);
    };

    $scope.draftMessageFromDraft = function () {
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            $scope.receiverId.push($scope.ReceiverIdArray[i].receiverId);
        }
        angular.forEach($scope.msgLoadingImg.data, function (val, key) {
            $scope.geDraftMsgData.image.push(val);
        });
        angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
            $scope.geDraftMsgData.attachment.push(val);
        });
        $scope.geDraftMsgData.receiverId = $scope.receiverId;
        if (!$scope.geDraftMsgData.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.geDraftMsgData.msg && !$scope.geDraftMsgData.image[0] && !$scope.geDraftMsgData.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.geDraftMsgData.disabled) {
                return false;
            }
            $scope.geDraftMsgData.disabled = true;
            Service.draftMsg($scope.geDraftMsgData).then(function (res) {
                $scope.geDraftMsgData.disabled = false;
                swal('Success', res.data.response, 'success').then(function () {
                    $state.reload();
                }, function () {
                });
            }, function (res) {
                $scope.geDraftMsgData.disabled = false;
                swal('Error', res.data.response, 'error');
            })
        }
    };


    //----------------------------------------------------draft---------------------------------------------------//

    //----------------------------------------------------star---------------------------------------------------//

    $scope.StartedData = {};
    $scope.startedMsg = function (msgId) {
        $scope.StartedData.msgId = msgId;
        Service.startedMsg($scope.StartedData).then(function (res) {
            if ($state.current.name == 'index.messages.inbox') {
                $scope.getInboxMsgs();
            }
            if ($state.current.name == 'index.messages.sent') {
                $scope.getSentMsgs();
            }
            if ($state.current.name == 'index.messages.draft') {
                $scope.getDraftMsgs();
            }
            if ($state.current.name == 'index.messages.started') {
                $scope.getStartedMsgs();
            } else {
                $scope.getDataIntoLabel();
            }
        }, function (res) {
        });
    };

    $scope.getStartedData = [];
    $scope.starPagination = {};
    $scope.starPagination.limit = '' + 10 + '';
    $scope.starPagination.pageNo = 1;

    $scope.starStartNo = (parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo - 1)) + 1;
    $scope.starEndNo = parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo);

    $scope.getStartedMsgs = function () {
        if ($scope.starPagination.disabled) {
            return false;
        }
        $scope.deleteSentMessageObj.thread_id = [];
        $scope.deleteStarMessageObj.thread_id = [];
        $scope.deleteDraftMessageObj.thread_id = [];
        $scope.deleteInboxMessageObj.thread_id = [];
        $scope.messageSearch = false;
        $scope.starPagination.disabled = true;
        $scope.loadingMessage = true;
        Service.getStartedMsg($scope.starPagination.limit, parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo - 1)).then(function (res) {
            $scope.getStartedData = res.data.response;
            $scope.starCount = res.data.total;
            $scope.starPagination.maxPage = Math.ceil($scope.starCount / $scope.starPagination.limit);

            $scope.starStartNo = (parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo - 1)) + 1;
            $scope.starEndNo = parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo);

            $scope.starMsg = false;
            $scope.starPagination.disabled = false;
            $scope.loadingMessage = false;
        }, function (res) {
            $scope.noStartedData = res.data.response;
            if ($scope.noStartedData == "Not Found") {
                $scope.starMsg = true;
            } else {
                $scope.starMsg = false;
            }
            $scope.getStartedData = [];
            $scope.starPagination.disabled = false;
            $scope.loadingMessage = false;
        });
    };

    $scope.starBackward = function () {
        if ($scope.starPagination.disabled) {
            return false;
        }
        if ($scope.starPagination.pageNo > 1) {
            $scope.starPagination.disabled = true;
            Service.getStartedMsg($scope.starPagination.limit, parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo - 2)).then(function (res) {
                $scope.getStartedData = res.data.response;
                $scope.starMsg = false;

                $scope.starPagination.pageNo = $scope.starPagination.pageNo - 1;
                $scope.starStartNo = (parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo - 1)) + 1;
                $scope.starEndNo = parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo);

                $scope.starPagination.disabled = false;
            }, function (res) {
                $scope.noStartedData = res.data.response;
                if ($scope.noStartedData == "Not Found") {
                    $scope.starMsg = true;
                } else {
                    $scope.starMsg = false;
                }
                $scope.getStartedData = [];
                $scope.starPagination.disabled = false;
            });
            $scope.starStartNo = $scope.starPagination.pageNo + 1;
            $scope.starEndNo = $scope.starPagination.limit;
        }
    };

    $scope.starForward = function () {
        if ($scope.starPagination.disabled) {
            return false;
        }
        if ($scope.starPagination.pageNo < $scope.starPagination.maxPage) {
            $scope.starPagination.disabled = true;
            Service.getStartedMsg($scope.starPagination.limit, parseInt($scope.starPagination.limit) * $scope.starPagination.pageNo).then(function (res) {
                $scope.getStartedData = res.data.response;
                $scope.starMsg = false;
                $scope.starPagination.pageNo = $scope.starPagination.pageNo + 1;
                $scope.starStartNo = (parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo - 1)) + 1;
                $scope.starEndNo = parseInt($scope.starPagination.limit) * ($scope.starPagination.pageNo);
                $scope.starPagination.disabled = false;
            }, function (res) {
                $scope.noStartedData = res.data.response;
                if ($scope.noStartedData == "Not Found") {
                    $scope.starMsg = true;
                } else {
                    $scope.starMsg = false;
                }
                $scope.getStartedData = [];
                $scope.starPagination.disabled = false;
            });
            $scope.starStartNo = ($scope.starPagination.limit * $scope.starPagination.pageNo) + 1;
            $scope.starEndNo = ($scope.starPagination.limit * ($scope.starPagination.pageNo + 1));
        }
    };

    $scope.selectAllStarMsg = function () {
        $scope.deleteSentData.msgId = [];
        $("input[type='checkbox'][name='delete-msg']").prop('checked', true);
        for (var i = 0; i < $scope.getStartedData.length; i++) {
            $scope.deleteSentData.msgId.push($scope.getStartedData[i].msgId);
        }
        if ($scope.deleteSentData.msgId) {
            $scope.allStar = true;
        }
    };

    $scope.deselectAllStarMsg = function () {
        $scope.deleteSentData.msgId = [];
        $("input[type='checkbox'][name='delete-msg']").prop('checked', false);
        for (var i = 0; i < $scope.getStartedData.length; i++) {
            $scope.deleteSentData.msgId.splice($scope.getStartedData[i].msgId);
        }
        $scope.allStar = false;
    };

    $scope.getStarMsgData = [];
    $scope.getStarMsgDetail = function () {
        $scope.reply = false;
        Service.getStarMsgDetail($state.params.msgId).then(function (res) {
            $scope.getStarMsgData = res.data.response;
            $rootScope.starSubject = $scope.getStarMsgData.subject;
        }, function (res) {
            $scope.getStarMsgData = [];
        })
    };

    $scope.createLableData = {};
    $scope.CreateLabelName = function () {
        if ($scope.createLableData.disabled) {
            return false;
        }
        $scope.createLableData.disabled = true;
        Service.createLabel($scope.createLableData).then(function (res) {
            $scope.createLableData.disabled = false;
            $('#createLableModel').modal('hide');
            $scope.getLabels();
            $scope.createLableData.label = "";
            swal('Success', res.data.response, 'success');
        }, function (res) {
            $scope.createLableData.disabled = false;
        });
    };

    $scope.getLabelsData = [];
    $scope.getLabels = function () {
        Service.getLabel().then(function (res) {
            $scope.getLabelsData = res.data.response;
            $(document).ready(function () {
                $('#get-labels').multiselect();
            });
        }, function (res) {
            $scope.noDraftData = res.data.response;
            $scope.getLabelsData = [];
        })
    };

    $scope.lableInfoObj = {};
    $scope.labelDetailsModel = function (label) {
        $scope.lableInfoObj.label = label.label;
        $scope.lableInfoObj.labelId = label.labelId;
        $('#editLableModel').modal('show');
    };

    $scope.editLabelName = function () {
        if ($scope.lableInfoObj.disabled) {
            return false;
        }
        $scope.lableInfoObj.disabled = true;
        Service.editLabelName($scope.lableInfoObj).then(function (res) {
            $('#editLableModel').modal('hide');
            $scope.getLabels();
            swal('Success', res.data.response, 'success');
            $scope.lableInfoObj.disabled = false;
        }, function (res) {
            $scope.lableInfoObj.disabled = false;
        });
    };

    $scope.LabelsData = [];
    $scope.labelagination = {};
    $scope.labelagination.limit = 10;
    $scope.labelagination.pageNo = 0;
    $scope.labelStartNo = (10 * (($scope.labelagination.pageNo + 1) - 1)) + ($scope.labelagination.pageNo + 1);
    $scope.labelEndNo = (10 * ($scope.labelagination.pageNo + 1));
    $scope.getDataIntoLabel = function (limit) {
        $scope.showLableActions = false;
        $scope.loadingMessage = true;
        $scope.deleteSentMessageObj.thread_id = [];
        $scope.deleteStarMessageObj.thread_id = [];
        $scope.deleteDraftMessageObj.thread_id = [];
        $scope.deleteInboxMessageObj.thread_id = [];
        if (limit) {
            $scope.labelagination.limit = limit;
            $scope.labelStartNo = ($scope.labelagination.limit * (($scope.labelagination.pageNo + 1) - 1)) + ($scope.labelagination.pageNo + 1);
            $scope.labelEndNo = ($scope.labelagination.limit * ($scope.labelagination.pageNo + 1));
        }
        $scope.messageSearch = false;
        if ($state.params.labelId) {
            Service.getDataIntoLabel($state.params.labelId, $scope.labelagination.limit, $scope.labelagination.pageNo).then(function (res) {
                $scope.LabelsData = res.data.response;
                $scope.labelCount = res.data.total;
                $scope.loadingMessage = false;
                $scope.labelagination.maxPage = Math.ceil($scope.labelCount / $scope.labelagination.limit);
            }, function (res) {
                $scope.loadingMessage = false;
                $scope.noLabelData = res.data.response;
                $scope.LabelsData = [];
            })
        }
    };

    $scope.labelBackward = function () {
        if ($scope.labelagination.pageNo != 0) {
            if ($scope.labelagination.pageNo == $scope.labelagination.limit) {
                $scope.labelagination.pageNo = $scope.labelagination.pageNo - $scope.labelagination.limit;
            } else {
                $scope.labelagination.pageNo = ($scope.labelagination.pageNo * $scope.labelagination.limit) - $scope.labelagination.limit;
            }
            Service.getDataIntoLabel($state.params.labelId, $scope.labelagination.limit, $scope.labelagination.pageNo).then(function (res) {
                $scope.LabelsData = res.data.response;
            }, function (res) {
                $scope.noLabelData = res.data.response;
                $scope.LabelsData = [];
            });
            $scope.labelStartNo = $scope.labelagination.pageNo + 1;
            $scope.labelEndNo = $scope.labelagination.limit;
        }
    };

    $scope.labelForward = function () {
        if (($scope.labelagination.pageNo + 1) < $scope.labelagination.maxPage) {
            $scope.labelagination.pageNo = $scope.labelagination.pageNo + 1;
            Service.getDataIntoLabel($state.params.labelId, $scope.labelagination.limit, $scope.labelagination.pageNo * $scope.labelagination.limit).then(function (res) {
                $scope.LabelsData = res.data.response;
            }, function (res) {
                $scope.noLabelData = res.data.response;
                $scope.LabelsData = [];
            });
            $scope.labelStartNo = ($scope.labelagination.limit * $scope.labelagination.pageNo) + 1;
            $scope.labelEndNo = ($scope.labelagination.limit * ($scope.sentPagination.pageNo + 1));
        }
    };


    $scope.deleteLable = {};
    $scope.deleteLable.labelId = [];
    $scope.deleteLableName = function (labelId) {
        $scope.deleteLable.labelId[0] = labelId;
        Service.deleteLableName($scope.deleteLable).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
            }, function () {
            });
            $scope.getLabels();
        }, function (res) {
        });
    };

    $scope.selectAllLabelMsg = function () {
        $scope.deleteLabelData.ld_Id = [];
        $("input[type='checkbox'][name='delete-label-msg']").prop('checked', true);
        for (var i = 0; i < $scope.LabelsData.length; i++) {
            $scope.deleteLabelData.ld_Id.push($scope.LabelsData[i].ld_Id);
            $scope.labelMsgId.push($("input[name=delete-label-msg]:checked").attr('label'));
        }
        if ($scope.deleteLabelData.ld_Id) {
            $scope.allLabel = true;
        }
    };

    $scope.deselectAllLabelMsg = function () {
        $scope.deleteLabelData.ld_Id = [];
        $("input[type='checkbox'][name='delete-label-msg']").prop('checked', false);
        for (var i = 0; i < $scope.LabelsData.length; i++) {
            $scope.deleteLabelData.ld_Id.splice($scope.LabelsData[i].ld_Id);
            $scope.labelMsgId.splice($("input[name=delete-label-msg]:checked").attr('label'));
        }
        $scope.allLabel = false;
    };

    $scope.confirmForLabelMsg = function () {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see message!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteLableMsg();
        });
    };

    $scope.deleteLabelData = {};
    $scope.deleteLabelData.ld_Id = [];
    $scope.deleteLableMsg = function () {
        Service.deleteLableMsg($scope.deleteLabelData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $scope.getDataIntoLabel();
            }, function () {
            });
        }, function (res) {
        });
    };

    $scope.addLabelMsgIntoLabel = function (labelId) {
        $scope.addLableData.labelId = labelId;
        $scope.addLableData.msgId = $scope.labelMsgId;
        Service.addIntoLabel($scope.addLableData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $state.reload();
            }, function () {
            });
        }, function (res) {
        });
    };

    $scope.deleteConfirm = function (labelId) {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see this lable!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteLableName(labelId);
        })
    };

    $scope.geLabelMsgData = [];
    $scope.getLabelMsgDetail = function () {
        $scope.reply = false;

        Service.getInboxMsgDetail($state.params.msgId).then(function (res) {
            $scope.geLabelMsgData = res.data.response;
            $rootScope.lableSubject = $scope.geLabelMsgData.subject;
        }, function (res) {
            $scope.geLabelMsgData = [];
        });
    };

    //----------------------------------------------------sent-reply---------------------------------------------------//

    $scope.sentReplyData = {};

    $scope.hideRplyBox = function (getInboxMsgData) {
        $scope.reply = false;
        $scope.replyAll = false;
        $scope.ReceiverIdArray.splice(getInboxMsgData);
    };

    $scope.sentReplyData.smsStatus = 0;
    $scope.sentReplyData.smsAlertStatus = 0;
    $scope.sentReplyData.emailAlertStatus = 0;
    $scope.sentReplyData.parent_msgId = 0;
    $scope.sentReplyData.image = [];
    $scope.sentReplyData.attachment = [];
    $scope.sentRplyOfMessage = function (msgId) {
        $scope.sentReplyData.subject = msgId.subject;
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            if ($scope.ReceiverIdArray[i].id) {
                $scope.receiverId.push({'id': $scope.ReceiverIdArray[i].id, 'flag': 1});
            }
            if ($scope.ReceiverIdArray[i].groupId) {
                $scope.receiverId.push({'id': $scope.ReceiverIdArray[i].groupId, 'flag': 2});
            }
        }
        angular.forEach($scope.msgLoadingImg.data, function (val, key) {
            $scope.sentReplyData.image.push(val);
        });
        angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
            $scope.sentReplyData.attachment.push(val);
        });
        $scope.sentReplyData.receiverId = $scope.receiverId;
        if (!$scope.sentReplyData.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.sentReplyData.msg && !$scope.sentReplyData.image[0] && !$scope.sentReplyData.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.sentReplyData.disabled) {
                return false;
            }
            $scope.sentReplyData.disabled = true;
            Service.sendMsg($scope.sentReplyData).then(function (res) {
                for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
                    if ($scope.ReceiverIdArray[i].id) {
                        $scope.receiverId.splice({'id': $scope.ReceiverIdArray[i].id, 'flag': 1});
                    }
                    if ($scope.ReceiverIdArray[i].groupId) {
                        $scope.receiverId.splice({'id': $scope.ReceiverIdArray[i].groupId, 'flag': 2});
                    }
                }
                $scope.sentReplyData.disabled = false;
                $scope.reply = false;
                $scope.getInboxMsgDetail();
                $scope.getSentMsgDetail();
                swal('Success', res.data.response, 'success').then(function () {
                }, function () {
                });
            }, function () {
                $scope.sentReplyData.disabled = false;
            });
        }
    };

    $scope.getSentMsgData = [];
    $scope.getSentMsgDetail = function () {
        $scope.messageSearch = false;
        $scope.reply = false;
        Service.getSentMsgDetail($state.params.msgId).then(function (res) {
            $scope.getSentMsgData = res.data.response;
            $rootScope.sentSubject = $scope.getSentMsgData.subject;
        }, function (res) {
            $scope.getSentMsgData = [];
        })
    };

    $scope.rplyOnSent = function (getSentMsgData) {
        for (i = 0; i < getSentMsgData.receivers.length; i++) {
            $scope.ReceiverIdArray.splice(getSentMsgData.receivers[i]);
            $scope.ReceiverIdArray.push(getSentMsgData.receivers[i]);
        }
        $scope.reply = true;
        $scope.replyAll = true;
    };

    $scope.rplyAllOnSent = function (getSentMsgData) {
        $scope.reply = true;
        $scope.replyAll = true;
        $scope.userId = Storage.get('ecampus_auth', true).id;
        for (i = 0; i < getSentMsgData.receivers.length; i++) {
            $scope.ReceiverIdArray.splice(getSentMsgData.receivers[i]);
            if ($scope.userId == getSentMsgData.receivers[i].id) {
                $scope.ReceiverIdArray.splice(getSentMsgData.receivers[i].id);
            } else {
                $scope.ReceiverIdArray.push(getSentMsgData.receivers[i]);
            }
        }
    };


    //----------------------------------------------------sent-reply---------------------------------------------------//


    $scope.deleteInboxRplyData = {};
    $scope.deleteRplyMessageFromInbox = function (msgResId) {
        $scope.deleteInboxRplyData.msgResId = msgResId;
        Service.deleteInboxRply($scope.deleteInboxRplyData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $scope.getInboxMsgDetail();
            }, function () {
            });
        }, function (res) {
        });
    };

    //----------------------------------------------------Search bar------------------------------------------------//

    $scope.searchMessageResultData = [];
    $scope.searchBarData = {};
    $scope.searchBarData.limit = '10';
    $scope.searchBarData.pageNo = 1;
    $scope.searchBarData.offset = 1;
    $scope.messageSearch = false;
    $scope.searchOnMessage = function () {
        $scope.searchStartNo = (parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset - 1)) + 1;
        $scope.searchEndNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset);
        if ($scope.searchBarData.disabled) {
            return false;
        }
        if ($state.current.name == 'index.messages.inbox') {
            var state = 'inbox';
        }
        if ($state.current.name == 'index.messages.sent') {
            var state = 'sent';
        }
        if ($state.current.name == 'index.messages.draft') {
            var state = 'draft';
        }
        if ($state.current.name == 'index.messages.started') {
            var state = 'star';
        }
        if ($state.current.name == 'index.messages.label') {
            var state = 'label';
        }
        $scope.searchBarData.state = state;

        if ($state.params.labelId && $state.current.name == 'index.messages.label') {
            $scope.searchBarData.labelId = $state.params.labelId;
        }

        $scope.searchBarData.pageNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset - 1);

        $scope.searchBarData.disabled = true;

        Service.searchOnMessage($scope.searchBarData).then(function (res) {
            $scope.messageSearch = true;
            $scope.searchBarData.disabled = false;
            $scope.searchMessageResultData = res.data.response;
            $scope.searchMsgCount = res.data.total;
            $scope.searchResult = $scope.searchBarData.search_text;
            $scope.searchBarData.maxPage = Math.ceil($scope.searchMsgCount / $scope.searchBarData.limit);
            $scope.searchStartNo = (parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset - 1)) + 1;
            $scope.searchEndNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset);
            setTimeout(function () {
                document.getElementById("search_message").focus();
            }, 1500);
        }, function (res) {
            $scope.searchMessageResultData = [];
            $scope.messageSearch = true;
            $scope.searchResult = $scope.searchBarData.search_text;
            $scope.searchBarData.disabled = false;
        });
    };

    $scope.searchBackward = function () {
        if ($scope.searchBarData.disabled) {
            return false;
        }
        if ($scope.searchBarData.offset > 0) {
            $scope.searchBarData.disabled = true;
            $scope.searchBarData.pageNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset - 2);
            Service.searchOnMessage($scope.searchBarData).then(function (res) {
                $scope.messageSearch = true;
                $scope.searchMessageResultData = res.data.response;
                $scope.searchMsgCount = res.data.total;
                $scope.searchBarData.offset = $scope.searchBarData.offset - 1;
                $scope.searchStartNo = (parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset - 1)) + 1;
                $scope.searchEndNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset);
                $scope.searchBarData.disabled = false;
            }, function (res) {
                $scope.searchBarData.disabled = false;
                $scope.searchMessageResultData = [];
            });
        }
    };

    $scope.searchForward = function () {
        if ($scope.searchBarData.disabled) {
            return false;
        }
        if ($scope.searchBarData.offset < $scope.searchBarData.maxPage) {
            $scope.searchBarData.pageNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset);
            $scope.searchBarData.disabled = true;
            Service.searchOnMessage($scope.searchBarData).then(function (res) {
                $scope.messageSearch = true;
                $scope.searchBarData.disabled = false;
                $scope.searchMessageResultData = res.data.response;
                $scope.searchMsgCount = res.data.total;
                $scope.searchBarData.offset = $scope.searchBarData.offset + 1;
                $scope.searchStartNo = (parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset - 1)) + 1;
                $scope.searchEndNo = parseInt($scope.searchBarData.limit) * ($scope.searchBarData.offset);
            }, function (res) {
                $scope.searchBarData.disabled = false;
                $scope.searchMessageResultData = [];
            });
        }
    };


    //----------------------------------------------------Search bar------------------------------------------------//

    //*********************function to print message****************************//
    $scope.printMessageBody = function (msg_id) {
        var userInfo = 'userInfo' + msg_id;
        var userDetail = document.getElementById(userInfo).innerHTML;
        var header = $('#headerSection').html();
        var popupWinindow = window.open('', '_blank', 'width=600,height=700,scrollbars=yes,menubar=no,toolbar=no,location=no,status=no,titlebar=no');
        popupWinindow.document.head.innerHTML = '<head>' + header + '</head>';
        popupWinindow.document.body.innerHTML = '<body><div class="col-md-12" style="border: 2px solid #d1d1d1;padding: 10px">' + userDetail + '</div></body>';
        popupWinindow.document.close();
        popupWinindow.focus();
        popupWinindow.print();
        popupWinindow.close();
    };
    //*********************function to print message****************************//

    $scope.backUpMessage = function (msg_id) {
        Service.backUpMessage({'msg_id': msg_id}).then(function (res) {
            console.log(res);
        }, function (res) {
            console.log(res);
        });
    };

    //*************************function for discrad message*************************************//
    $scope.discardMsg = function (index) {
        if ($scope.sendMessageData) {
            $scope.sendMessageData.parent_msgId = "";
            $scope.sendMessageData.msgId = "";
            $scope.sendMessageData.smsStatus = "";
            $scope.sendMessageData.smsAlertStatus = "";
            $scope.sendMessageData.emailAlertStatus = "";
            $scope.sendMessageData.image = "";
            $scope.sendMessageData.attachment = "";
            $scope.sendMessageData.receiverId = "";
            $scope.sendMessageData.msg = "";
            $scope.sendMessageData.subject = "";
            $scope.ReceiverIdArray.splice(index, 1);
            $state.go('index.messages.inbox');
        }
    };
    //*************************function for discrad message*************************************//

    //************************functionalities of message group*************************//

    $scope.messageGroupsData = [];
    $scope.messageGroupsObj = {};
    $scope.messageGroupsObj.totalItems = "";
    $scope.messageGroupsObj.pageNo = 1;
    $scope.messageGroupsObj.itemsPerPage = '' + 20 + '';
    $scope.setMsgGrpPage = function (pageNo) {
        $scope.messageGroupsObj.pageNo = pageNo;
    };
    $scope.getMessageGroups = function () {
        $scope.messageGroupsObj.limit = $scope.messageGroupsObj.itemsPerPage;
        Service.getMessageGroups($scope.messageGroupsObj).then(function (res) {
            $scope.messageGroupsData = res.data.response;
            $scope.messageGroupsObj.totalItems = res.data.totalCount;
            resultLength = $scope.messageGroupsObj.totalItems;
        }, function (res) {
            $scope.messageGroupsData = [];
        });
    };

    $scope.editSingleGroup = {};
    $scope.singleMessgeGroupObj = {};
    $scope.singleMessgeGroupObj.totalItems = "";
    $scope.singleMessgeGroupObj.pageNo = 1;
    $scope.singleMessgeGroupObj.itemsPerPage = 20;
    $scope.setSinMsgGrpPage = function (pageNo) {
        $scope.singleMessgeGroupObj.pageNo = pageNo;
    };
    $scope.singleMessageGroup = function () {
        $scope.singleMessgeGroupObj.groupId = $state.params.groupId;
        $scope.singleMessgeGroupObj.limit = $scope.singleMessgeGroupObj.itemsPerPage;
        Service.singleMessageGroup($scope.singleMessgeGroupObj).then(function (res) {
            $scope.messageMememberData = res.data.response;
            $scope.singleMessageDetails = res.data.details[0];
            $scope.editSingleGroup.groupName = $scope.singleMessageDetails.groupName;
            $scope.editSingleGroup.accountType = '' + $scope.singleMessageDetails.accountType + '';
            $scope.singleMessgeGroupObj.totalItems = res.data.totalCount;
            resultLength = $scope.singleMessgeGroupObj.totalItems;
        }, function (res) {
        });
    };


    $scope.editMessageGroupSubmit = function () {
        if ($scope.editSingleGroup.disabled) {
            return false;
        }
        $scope.editSingleGroup.groupId = $state.params.groupId;
        $scope.editSingleGroup.disabled = true;
        Service.editMessageGroup($scope.editSingleGroup).then(function (res) {
            $scope.editSingleGroup.disabled = false;
            $scope.singleMessageGroup();
            $('#updateGroup').modal('hide');
        }, function (res) {
            $scope.editSingleGroup.disabled = false;
            $('#updateGroup').modal('hide');
        });
    };

    $scope.addNewGroupObj = {};
    $scope.addNewMessageGroup = function () {
        if ($scope.addNewGroupObj.disabled) {
            return false;
        }
        $scope.addNewGroupObj.disabled = true;
        Service.addNewMessageGroup($scope.addNewGroupObj).then(function (res) {
            $scope.addNewGroupObj.disabled = false;
            swal('Success', res.data.response, 'success').then(function () {
                $state.go('index.messages.add-group-member', {'groupId': res.data.groupId});
            });
        }, function (res) {
            $scope.addNewGroupObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.customGroupDetail = [];
    $scope.memberListData = [];
    $scope.getMemberList = function () {
        Service.getMemberList({'groupId': $state.params.groupId}).then(function (res) {
            $scope.customGroupDetail = res.data.response[0];
            $scope.memberListData = res.data.members;
        }, function (res) {
            $scope.customGroupDetail = [];
            $scope.memberListData = [];
        });
    };


    $scope.addNewMemeberObj = {};
    $scope.addNewMemeberObj.userId = [];
    $scope.selectAllGroupMembers = function (allMembers) {
        if (allMembers) {
            if ($scope.getStartedData) {
                for (var i = 0; i < $scope.searchMemberData.length; i++) {
                    $scope.addNewMemeberObj.userId.push($scope.searchMemberData[i].id);
                }
            }
        } else {
            $scope.addNewMemeberObj.userId = [];
        }
    };

    $scope.addNewMember = function () {
        $scope.addNewMemeberObj.groupId = $state.params.groupId;
        if ($scope.addNewMemeberObj.disabled) {
            return false;
        }
        $scope.addNewMemeberObj.disabled = true;
        Service.addNewMember($scope.addNewMemeberObj).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $state.reload();
            }, function () {
                $state.reload();
            });
            $scope.addNewMemeberObj.disabled = false;
            $scope.addNewMemeberObj.userId = [];
            $scope.searchMemberObj.name = '';
        }, function (res) {
            $scope.addNewMemeberObj.disabled = false;
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.removeGroupMemberData = {};
    $scope.removeGroupMember = function (userId) {
        swal({
            title: 'Are you sure',
            text: 'Do you want to remove ?',
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes'
        }).then(function () {
            $scope.removeGroupMemberData.groupId = $scope.customGroupDetail.groupId;
            $scope.removeGroupMemberData.userId = userId;
            if ($scope.removeGroupMemberData.disabled) {
                return false;
            }
            $scope.removeGroupMemberData.disabled = true;
            Service.removeGroupMember($scope.removeGroupMemberData).then(function (res) {
                $scope.getMemberList();
                $scope.removeGroupMemberData.disabled = false;
            }, function (res) {
                $scope.removeGroupMemberData.disabled = false;
                swal('Error', res.data.message, 'error');
            });
        })
    };

    $scope.searchMemberObj = {};
    $scope.searchMemberObj.totalItems = "";
    $scope.searchMemberObj.pageNo = 1;
    $scope.searchMemberObj.maxSize = 5;
    $scope.searchMemberObj.itemsPerPage = 20;
    $scope.searchMem = function (pageNo) {
        $scope.searchMemberObj.pageNo = pageNo;
    };
    $scope.searchMember = function () {
        $scope.searchMemberObj.groupId = $state.params.groupId;
        $scope.searchMemberObj.limit = $scope.searchMemberObj.itemsPerPage;
        Service.searchMember($scope.searchMemberObj).then(function (res) {
            $scope.searchMemberData = res.data.response;
            $scope.searchMemberObj.totalItems = res.data.totalCount;
            resultLength = $scope.searchMemberObj.totalItems;
        });
    };

    $scope.allUserGroupsObj = {};
    $scope.allUserGroupsObj.totalItems = "";
    $scope.allUserGroupsObj.pageNo = 1;
    $scope.allUserGroupsObj.maxSize = 5;
    $scope.allUserGroupsObj.itemsPerPage = 20;
    $scope.allUserPage = function (pageNo) {
        $scope.searchMemberObj.pageNo = pageNo;
    };
    $scope.getAllUserGroups = function () {
        Service.getAllUserGroups($scope.allUserGroupsObj).then(function (res) {
            $scope.allUserGroupData = res.data.response;
        });
    };

    //************************functionalities of message group*************************//
    $scope.signature = function () {
        $scope.composeMessageObj.body =
            '<br>' +
            '<br>' +
            '<div>------------------------------------------------------------------------</div>' +
            '<div>' + Storage.get('ecampus_auth', true).fullname + '</div>' +
            '<div>' + Storage.get('ecampus_auth', true).username + '</div>'
    };

    $scope.composeMessage = function () {
        $scope.messageSearch = false;
        $state.go('index.messages.compose');
        $scope.ReceiverIdArray.splice($scope.forwardReceiver);
    };

    //***********************************************************************NEW**********************************************************************//

    //******************************************Compose Message******************************************//
    $scope.composeMessageSubmit = function (draftMessage) {
        if (draftMessage) {
            $scope.composeMessageObj.draftMessage = 1;
        } else {
            $scope.composeMessageObj.draftMessage = 0;
        }
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            if ($scope.ReceiverIdArray[i].id) {
                $scope.composeMessageObj.receiverId.push({'id': $scope.ReceiverIdArray[i].id, 'flag': 1});
            }
            if ($scope.ReceiverIdArray[i].groupId) {
                $scope.composeMessageObj.receiverId.push({'id': $scope.ReceiverIdArray[i].groupId, 'flag': 2});
            }
        }
        if (!$scope.composeMessageObj.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.composeMessageObj.body && !$scope.composeMessageObj.image[0] && !$scope.composeMessageObj.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.composeMessageObj.disabled) {
                return false;
            }
            angular.forEach($scope.msgLoadingImg.data, function (val, key) {
                $scope.composeMessageObj.image.push(val);
            });
            angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
                $scope.composeMessageObj.attachment.push(val);
            });
            $scope.composeMessageObj.disabled = true;
            Service.composeMessage($scope.composeMessageObj).then(function (res) {
                $scope.composeMessageObj = {disabled: false, image: [], receiverId: [], attachment: []};
                $scope.msgLoadingImg.data = [];
                $scope.msgLoadingAttechment.data = [];
                $scope.signature();
                swal('Success', res.data.response, 'success');
                $state.go('index.messages.inbox');
            }, function (res) {
                $scope.composeMessageObj.disabled = false;
                swal('Error', res.data.message, 'error');
            });
        }
    };
    //******************************************Compose Message******************************************//

    //******************************************Send Draft Message***************************************//
    $scope.sendDraftMessage = function (draftMessage) {
        if (draftMessage) {
            $scope.geDraftMsgData.draftMessage = 1;
        } else {
            $scope.geDraftMsgData.draftMessage = 0;
        }

        $scope.geDraftMsgData.receiverId = [];
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            if ($scope.ReceiverIdArray[i].id) {
                $scope.geDraftMsgData.receiverId.push({'id': $scope.ReceiverIdArray[i].id, 'flag': 1});
            } else if ($scope.ReceiverIdArray[i].groupId) {
                $scope.geDraftMsgData.receiverId.push({'id': $scope.ReceiverIdArray[i].groupId, 'flag': 2});
            } else if ($scope.ReceiverIdArray[i].recipient_id) {
                $scope.geDraftMsgData.receiverId.push({'id': $scope.ReceiverIdArray[i].recipient_id, 'flag': 1});
            }
        }
        if (!$scope.geDraftMsgData.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.geDraftMsgData.body && !$scope.geDraftMsgData.image[0] && !$scope.geDraftMsgData.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.geDraftMsgData.disabled) {
                return false;
            }
            angular.forEach($scope.msgLoadingImg.data, function (val, key) {
                $scope.geDraftMsgData.image.push(val);
            });
            angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
                $scope.geDraftMsgData.attachment.push(val);
            });
            $scope.geDraftMsgData.disabled = true;
            Service.composeMessage($scope.geDraftMsgData).then(function (res) {
                $scope.geDraftMsgData = {};
                swal('Success', res.data.response, 'success').then(function () {
                    $state.go('index.messages.draft');
                }, function () {
                    $state.go('index.messages.draft');
                });
            }, function (res) {
                $scope.geDraftMsgData.disabled = false;
                swal('Error', res.data.message, 'error');
            });
        }
    };
    //******************************************Send Draft Message***************************************//

    //***************************************Sent Reply**************************************************//
    $scope.sentReplyMessageObj = {};
    $scope.showRplyBox = function (getInboxMsgData) {
        $scope.ReceiverIdArray = [];
        $scope.ReceiverIdArray.push({'id': getInboxMsgData.sender_id, 'fullName': getInboxMsgData.fullName});
        $scope.sentReplyMessageObj.send_type = 1;
        $scope.sentReplyMessageObj.image = [];
        $scope.sentReplyMessageObj.attachment = [];
        $scope.sentReplyMessageObj.receiverId = [];
        $scope.sentReplyMessageObj.msg_id = getInboxMsgData.msg_id;
        $scope.sentReplyMessageObj.thread_id = getInboxMsgData.thread_id;
        var msgHtml = document.createElement('HTML');
        $(msgHtml).html(getInboxMsgData.body);
        var msgBody = $(msgHtml).find('body').html();
        $scope.sentReplyMessageObj.body =
            '<br>' +
            '<br>' +
            '<div class="forward-message-box"> On ' + moment(getInboxMsgData.created_on, 'X').format('MMM D, YYYY, h:mm A') + ', ' + getInboxMsgData.fullName + '(' + getInboxMsgData.username + ')' + ' wrote: </div>' +
            '<div class="forward-message-body">' + msgBody + '</div>' +
            '<div style="margin-top: 10px;">------------------------------------------------------------------------</div>' +
            '<div>' + Storage.get('ecampus_auth', true).fullname + '</div>' +
            '<div>' + Storage.get('ecampus_auth', true).username + '</div>';
        $scope.reply = true;
        $scope.replyAll = false;
        $("html, body").animate({scrollTop: $(document).height()}, 1000);
    };

    $scope.showRplyAll = function (getInboxMsgData) {
        $scope.sentReplyMessageObj.send_type = 1;
        $scope.sentReplyMessageObj.receiverId = [];
        $scope.sentReplyMessageObj.image = [];
        $scope.sentReplyMessageObj.attachment = [];
        $scope.sentReplyMessageObj.msg_id = getInboxMsgData.msg_id;
        $scope.sentReplyMessageObj.thread_id = getInboxMsgData.thread_id;
        $scope.ReceiverIdArray.push({'id': getInboxMsgData.sender_id, 'fullName': getInboxMsgData.fullName});
        $scope.userId = Storage.get('ecampus_auth', true).id;
        for (i = 0; i < getInboxMsgData.receivers.length; i++) {
            if ($scope.userId == getInboxMsgData.receivers[i].recipient_id) {
                $scope.ReceiverIdArray.splice(getInboxMsgData.receivers[i].recipient_id);
            } else {
                $scope.ReceiverIdArray.push({
                    'id': getInboxMsgData.receivers[i].recipient_id,
                    'fullName': getInboxMsgData.receivers[i].fullName
                });
            }
        }
        var msgHtml = document.createElement('HTML');
        $(msgHtml).html(getInboxMsgData.body);
        var msgBody = $(msgHtml).find('body').html();
        $scope.sentReplyMessageObj.body =
            '<br>' +
            '<br>' +
            '<div class="forward-message-box"> On' + ' ' + moment(getInboxMsgData.created_on, 'X').format('MMM D YYYY, h:mm A') + ', ' + getInboxMsgData.fullName + '(' + getInboxMsgData.username + ')' + ' wrote:</div>' +
            '<div class="forward-message-body">' + msgBody + '</div>' +
            '<div style="margin-top: 10px;">------------------------------------------------------------------------</div>' +
            '<div>' + Storage.get('ecampus_auth', true).fullname + '</div>' +
            '<div>' + Storage.get('ecampus_auth', true).username + '</div>';
        $scope.reply = true;
        $scope.replyAll = true;
        $("html, body").animate({scrollTop: $(document).height()}, 1000);
    };

    $scope.sentRelyMessage = function () {
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            if ($scope.ReceiverIdArray[i].id) {
                $scope.sentReplyMessageObj.receiverId.push({'id': $scope.ReceiverIdArray[i].id, 'flag': 1});
            }
            if ($scope.ReceiverIdArray[i].groupId) {
                $scope.sentReplyMessageObj.receiverId.push({'id': $scope.ReceiverIdArray[i].groupId, 'flag': 2});
            }
        }
        angular.forEach($scope.msgLoadingImg.data, function (val, key) {
            $scope.sentReplyMessageObj.image.push(val);
        });
        angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
            $scope.sentReplyMessageObj.attachment.push(val);
        });
        if (!$scope.sentReplyMessageObj.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.sentReplyMessageObj.body && !$scope.sentReplyMessageObj.image[0] && !$scope.sentReplyMessageObj.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.sentReplyMessageObj.disabled) {
                return false;
            }
            $scope.sentReplyMessageObj.disabled = true;
            Service.composeMessage($scope.sentReplyMessageObj).then(function (res) {
                $scope.sentReplyMessageObj.disabled = false;
                $scope.reply = false;
                $scope.getSingleMessage();
                $scope.sentReplyMessageObj.image = [];
                $scope.sentReplyMessageObj.receiverId = [];
                $scope.sentReplyMessageObj.attachment = [];
                $scope.msgLoadingImg.data = [];
                $scope.msgLoadingAttechment.data = [];
                swal('Success', res.data.response, 'success').then(function () {
                });
            }, function (res) {
                $scope.sentReplyMessageObj.disabled = false;
                $scope.sentReplyMessageObj.image = [];
                $scope.sentReplyMessageObj.receiverId = [];
                $scope.sentReplyMessageObj.attachment = [];
                $scope.msgLoadingImg.data = [];
                $scope.msgLoadingAttechment.data = [];
                swal('Error', res.data.message, 'error');
            });
        }
    };
    //***************************************Sent Reply**************************************************//

    //*******************************************Forward Message******************************************//
    $scope.forwardMessageObj = {};
    $scope.forwardMessageObj.image = [];
    $scope.forwardMessageObj.attachment = [];
    $scope.showForwardBox = function (getInboxMsgData) {
        $scope.reply = true;
        $scope.forWardAtt = getInboxMsgData.attachment;
        $scope.revceiverArray = [];
        $scope.ReceiverIdArray = [];
        $scope.forwardMessageObj.send_type = 2;
        $scope.forwardMessageObj.receiverId = [];
        for (var i = 0; i < getInboxMsgData.attachment.length; i++) {
            if (getInboxMsgData.attachment[i].status == 0) {
                $scope.forwardMessageObj.attachment.push(getInboxMsgData.attachment[i].attachment);
            }
            if (getInboxMsgData.attachment[i].status == 1) {
                $scope.forwardMessageObj.image.push(getInboxMsgData.attachment[i].attachment);
            }
        }
        $scope.forwardMessageObj.msg_id = getInboxMsgData.msg_id;
        $scope.forwardMessageObj.thread_id = getInboxMsgData.thread_id;
        for (var r = 0; r < getInboxMsgData.receivers.length; r++) {
            $scope.revceiverArray.push(getInboxMsgData.receivers[r].fullName);
        }
        var msgHtml = document.createElement('HTML');
        $(msgHtml).html(getInboxMsgData.body);
        var msgBody = $(msgHtml).find('body').html();
        if (!msgBody) {
            msgBody = $(msgHtml).html();
        }
        $scope.forwardMessageObj.body =
            '<br>' +
            '<br>' +
            '<div class="forward-message-box">' +
            '<div>----------- Forwarded message -----------</div>' +
            '<b>From:</b>' + ' ' + getInboxMsgData.fullName + '<br>' +
            '<b>Date:</b>' + ' ' + moment(getInboxMsgData.created_on, 'X').format('MMM D , h:mm A') + '<br>' +
            '<b>Subject:</b>' + ' ' + getInboxMsgData.subject + '<br>' +
            '<b>To:</b>' + ' ' + $scope.revceiverArray.join(", ") +
            '</div>' +
            '<div class="forward-message-body">' + msgBody + '</div>' +
            '<div style="margin-top: 10px;">------------------------------------------------------------------------</div>' +
            '<div>' + Storage.get('ecampus_auth', true).fullname + '</div>' +
            '<div>' + Storage.get('ecampus_auth', true).username + '</div>';

        $scope.forward = true;
        $("html, body").animate({scrollTop: $(document).height()}, 1000);
    };

    $scope.forwardMessage = function () {
        for (i = 0; i < $scope.ReceiverIdArray.length; i++) {
            if ($scope.ReceiverIdArray[i].id) {
                $scope.forwardMessageObj.receiverId.push({'id': $scope.ReceiverIdArray[i].id, 'flag': 1});
            }
            if ($scope.ReceiverIdArray[i].groupId) {
                $scope.forwardMessageObj.receiverId.push({'id': $scope.ReceiverIdArray[i].groupId, 'flag': 2});
            }
        }
        angular.forEach($scope.msgLoadingImg.data, function (val, key) {
            $scope.forwardMessageObj.image.push(val);
        });
        angular.forEach($scope.msgLoadingAttechment.data, function (val, key) {
            $scope.forwardMessageObj.attachment.push(val);
        });
        if (!$scope.forwardMessageObj.receiverId[0]) {
            swal('Error', 'Please specify at least one recipient.', 'error');
        } else if (!$scope.forwardMessageObj.body && !$scope.forwardMessageObj.image[0] && !$scope.forwardMessageObj.attachment[0]) {
            swal('Error', 'Message can\'t be sent without message body or attachment', 'error');
        } else {
            if ($scope.forwardMessageObj.disabled) {
                return false;
            }
            $scope.forwardMessageObj.disabled = true;
            Service.composeMessage($scope.forwardMessageObj).then(function (res) {
                $scope.forwardMessageObj.disabled = false;
                $scope.reply = false;
                $scope.getSingleMessage();
                $scope.forwardMessageObj.image = [];
                $scope.forwardMessageObj.receiverId = [];
                $scope.forwardMessageObj.attachment = [];
                $scope.msgLoadingImg.data = [];
                $scope.msgLoadingAttechment.data = [];
                swal('Success', res.data.response, 'success').then(function () {
                });
            }, function (res) {
                $scope.forwardMessageObj.disabled = false;
                $scope.forwardMessageObj.image = [];
                $scope.forwardMessageObj.receiverId = [];
                $scope.forwardMessageObj.attachment = [];
                $scope.msgLoadingImg.data = [];
                $scope.msgLoadingAttechment.data = [];
                swal('Error', res.data.message, 'error');
            });
        }
    };
    //*******************************************Forward Message*****************************************//

    //*******************************************Delete Message*****************************************//


    $scope.selectAllMessage = function (testCheck) {

        if (testCheck == 1) {
            $scope.showInboxActions = true;
            $scope.deleteInboxMessageObj.thread_id = [];
            for (var i = 0; i < $scope.getInboxData.length; i++) {
                $scope.deleteInboxMessageObj.thread_id.push($scope.getInboxData[i].thread_id);
            }
            $scope.deleteMessagesObj.thread_id = $scope.deleteInboxMessageObj.thread_id;
            $scope.moveMessageObj.thread_id = $scope.deleteInboxMessageObj.thread_id;
        } else if (testCheck == 2) {
            $scope.showSentActions = true;
            $scope.deleteSentMessageObj.thread_id = [];
            for (var i = 0; i < $scope.getSentData.length; i++) {
                $scope.deleteSentMessageObj.thread_id.push($scope.getSentData[i].thread_id);
                $scope.addLableData.msgId.push($scope.getSentData[i].msgId);
            }
            $scope.deleteMessagesObj.thread_id = $scope.deleteSentMessageObj.thread_id;
            $scope.moveMessageObj.thread_id = $scope.deleteSentMessageObj.thread_id;
        } else if (testCheck == 3) {
            $scope.shoDraftActions = true;
            $scope.deleteDraftMessageObj.thread_id = [];
            for (var i = 0; i < $scope.getDraftData.length; i++) {
                $scope.deleteDraftMessageObj.thread_id.push($scope.getDraftData[i].thread_id);
                $scope.addLableData.msgId.push($scope.getDraftData[i].msgId);
            }
            $scope.deleteMessagesObj.thread_id = $scope.deleteDraftMessageObj.thread_id;
            $scope.moveMessageObj.thread_id = $scope.deleteDraftMessageObj.thread_id;
        } else if (testCheck == 4) {
            $scope.showStarActions = true;
            $scope.deleteStarMessageObj.thread_id = [];
            for (var i = 0; i < $scope.getStartedData.length; i++) {
                $scope.deleteStarMessageObj.thread_id.push($scope.getStartedData[i].thread_id);
            }
            $scope.deleteMessagesObj.thread_id = $scope.deleteStarMessageObj.thread_id;
            $scope.moveMessageObj.thread_id = $scope.deleteStarMessageObj.thread_id;
        } else if (testCheck == 5) {
            $scope.showLableActions = true;
            $scope.deleteLableMessageObj.thread_id = [];
            for (var i = 0; i < $scope.LabelsData.length; i++) {
                $scope.deleteLableMessageObj.thread_id.push($scope.LabelsData[i].thread_id);
            }
            $scope.deleteMessagesObj.thread_id = $scope.deleteLableMessageObj.thread_id;
            $scope.moveToInboxObj.thread_id = $scope.deleteLableMessageObj.thread_id;
        } else if (testCheck == 6) {
            $scope.showSearchActions = true;
            $scope.deleteSearchMessageObj.thread_id = [];
            for (var i = 0; i < $scope.searchMessageResultData.length; i++) {
                $scope.deleteSearchMessageObj.thread_id.push($scope.searchMessageResultData[i].thread_id);
            }
            $scope.deleteMessagesObj.thread_id = $scope.deleteSearchMessageObj.thread_id;
            $scope.moveMessageObj.thread_id = $scope.deleteSearchMessageObj.thread_id;

        } else {
            $scope.deleteInboxMessageObj.thread_id = [];
            $scope.deleteSentMessageObj.thread_id = [];
            $scope.deleteStarMessageObj.thread_id = [];
            $scope.deleteDraftMessageObj.thread_id = [];
            $scope.deleteLableMessageObj.thread_id = [];
            $scope.deleteSearchMessageObj.thread_id = [];
            $scope.showInboxActions = false;
            $scope.showSentActions = false;
            $scope.shoDraftActions = false;
            $scope.showStarActions = false;
            $scope.showLableActions = false;
            $scope.showSearchActions = false;
        }
    };

    $scope.getCheckboxValue = function (index) {
        var chkBoxArray = [];

        if ($scope.deleteInboxMessageObj) {
            angular.forEach($scope.deleteInboxMessageObj.thread_id, function (val, key) {
                if (val) {
                    chkBoxArray.push(val);
                }
                $scope.moveMessageObj.thread_id = chkBoxArray;
                $scope.deleteMessagesObj.thread_id = $scope.deleteInboxMessageObj.thread_id;
            });
        }

        if ($scope.deleteSentMessageObj) {
            angular.forEach($scope.deleteSentMessageObj.thread_id, function (val, key) {
                if (val) {
                    chkBoxArray.push(val);
                }
                $scope.deleteMessagesObj.thread_id = $scope.deleteSentMessageObj.thread_id;
            });
        }

        if ($scope.deleteDraftMessageObj) {
            angular.forEach($scope.deleteDraftMessageObj.thread_id, function (val, key) {
                if (val) {
                    chkBoxArray.push(val);
                }
                $scope.deleteMessagesObj.thread_id = $scope.deleteDraftMessageObj.thread_id;
            });
        }

        if ($scope.deleteStarMessageObj) {
            angular.forEach($scope.deleteStarMessageObj.thread_id, function (val, key) {
                if (val) {
                    chkBoxArray.push(val);
                }
                $scope.deleteMessagesObj.thread_id = $scope.deleteStarMessageObj.thread_id;
            });
        }

        if ($scope.deleteLableMessageObj) {
            angular.forEach($scope.deleteLableMessageObj.thread_id, function (val, key) {
                if (val) {
                    chkBoxArray.push(val);
                }
                $scope.moveToInboxObj.thread_id = chkBoxArray;
                $scope.deleteMessagesObj.thread_id = $scope.deleteLableMessageObj.thread_id;
            });
        }

        if ($scope.deleteSearchMessageObj) {
            angular.forEach($scope.deleteSearchMessageObj.thread_id, function (val, key) {
                if (val) {
                    chkBoxArray.push(val);
                }
                $scope.moveMessageObj.thread_id = chkBoxArray;
                $scope.deleteMessagesObj.thread_id = $scope.deleteSearchMessageObj.thread_id;
            });
        }


        if (chkBoxArray.length > 0) {
            $scope.showInboxActions = true;
            $scope.showSentActions = true;
            $scope.shoDraftActions = true;
            $scope.showStarActions = true;
            $scope.showLableActions = true;
            $scope.showSearchActions = true;
        } else {
            $scope.showInboxActions = false;
            $scope.showSentActions = false;
            $scope.shoDraftActions = false;
            $scope.showStarActions = false;
            $scope.showLableActions = false;
            $scope.showSearchActions = false;
        }
    };

    $scope.deleteMessage = function (type, msg_id) {
        $scope.deleteMessagesObj.type = type;
        if (msg_id) {
            $scope.deleteMessagesObj.msg_id = msg_id;
            $scope.deleteMessagesObj.thread_id = [];
        }
        Service.deleteMessage($scope.deleteMessagesObj).then(function (res) {
            swal('Success', res.data.response, 'success');
            $state.reload();
            if ($state.current.name == 'index.messages.inbox') {
                $scope.getInboxMsgs();
            }
            if ($state.current.name == 'index.messages.sent') {
                $scope.getSentMsgs();
            }
            if ($state.current.name == 'index.messages.draft') {
                $scope.getDraftMsgs();
            }
            if ($state.current.name == 'index.messages.started') {
                $scope.getStartedMsgs();
            }
            if ($state.current.name == 'index.messages.inbox-message' || $state.current.name == 'index.messages.sent-message' || $state.current.name == 'index.messages.star-message') {
                $scope.getSingleMessage();
            }
        }, function (res) {
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.confirmForDeleteMessage = function (type, msg_id) {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see message!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteMessage(type, msg_id);
        });
    };
    //*******************************************Delete Message*****************************************//

    //*******************************************Single Message*****************************************//
    $scope.getSingleMessageData = [];
    $scope.getSingleMessage = function () {
        $scope.subjectName = '';
        $scope.getSingleMessageData = [];
        $scope.messageSearch = false;
        $scope.reply = false;
        $scope.loadingMessage = true;
        Service.getSingleMessage({'thread_id': $state.params.msgId}).then(function (res) {
            $scope.getSingleMessageData = res.data.response;

            for (var i = 0; i < $scope.getSingleMessageData.length; i++) {
                var ind = $scope.getSingleMessageData[i].body.search('forward-message-box');
                var ele = document.createElement('div');
                ele.innerHTML = $scope.getSingleMessageData[i].body;
                $.each($(ele).find('div.forward-message-box'), function (i, v) {
                    $(this).append('<div class="mce-ellipsis" onclick="showMessage(this)">...</div>')
                });

                $scope.getSingleMessageData[i].bodyDisplay = $(ele).html();
                $scope.getSingleMessageData[i].bodyText = ($scope.getSingleMessageData[i].body.replace(/<\/?[^>]+(>|$)/g, "").replace(/-/g, "")).trim();

                if ($scope.getSingleMessageData[i].receivers.length > 3) {
                    var data = {
                        'value': $scope.getSingleMessageData[i].receivers.slice(0, 3),
                        'status': true,
                        'more': $scope.getSingleMessageData[i].receivers.length - 3
                    };
                    $scope.getSingleMessageData[i].moreReceivers = data;
                } else {
                    var data = {
                        'status': false
                    };
                    $scope.getSingleMessageData[i].moreReceivers = data;
                }
            }

            if ($scope.getSingleMessageData.length) {
                $scope.getSingleMessageData[$scope.getSingleMessageData.length - 1].show = true;
            }

            $scope.subjectName = res.data.subject;
            $scope.olderMessages = res.data.old;
            $scope.newerMessages = res.data.new;
            $scope.positionOfMessage = res.data.position;
            $scope.totalOfMessage = res.data.total;
            $scope.darftMessageData = res.data.draft_message;
            $scope.loadingMessage = false;

            if (!$scope.getSingleMessageData[0] && !$scope.darftMessageData) {
                $state.go('index.messages.inbox');
            }

            if ($scope.getSingleMessageData[0]) {
                $rootScope.messageSubject = $scope.getSingleMessageData[0].subject;
            } else if ($scope.darftMessageData) {
                $rootScope.messageSubject = $scope.darftMessageData.subject;
            }
            $scope.geDraftMsgData = {};
            if ($scope.darftMessageData) {
                $scope.ReceiverIdArray = [];
                $scope.msgLoadingImg.data = [];
                $scope.msgLoadingAttechment.data = [];
                $scope.geDraftMsgData.image = [];
                $scope.geDraftMsgData.attachment = [];
                $scope.geDraftMsgData.body = $scope.darftMessageData.body;
                $scope.geDraftMsgData.subject = $scope.darftMessageData.subject;
                $scope.geDraftMsgData.thread_id = $scope.darftMessageData.thread_id;
                $scope.geDraftMsgData.draft_msg_id = $scope.darftMessageData.msg_id;
                $rootScope.draftSubject = $scope.darftMessageData.subject;

                for (i = 0; i < $scope.darftMessageData.receivers.length; i++) {
                    $scope.ReceiverIdArray.push($scope.darftMessageData.receivers[i]);
                }

                for (j = 0; j < $scope.darftMessageData.attachment.length; j++) {
                    if ($scope.darftMessageData.attachment[j].status == 1) {
                        $scope.msgLoadingImg.data.push($scope.darftMessageData.attachment[j].attachment);
                    }
                    if ($scope.darftMessageData.attachment[j].status == 0) {
                        $scope.msgLoadingAttechment.data.push($scope.darftMessageData.attachment[j].attachment);
                    }
                }
            }

            $scope.getCountOfUnreadMsg();
        }, function (res) {
            $scope.loadingMessage = false;
            $scope.getSingleMessageData = [];
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.viewAllReceivers = function (obj) {
        $scope.messageReceivers = obj.receivers;
        $('#allReceiversModal').modal('show');
    };
    //*******************************************Single Message*****************************************//
    //*******************************************Move Message*****************************************//

    $scope.moveMessage = function (labelId) {
        $scope.moveMessageObj.label_id = labelId;
        Service.moveMessage($scope.moveMessageObj).then(function (res) {
            swal('Success', res.data.response, 'success');
            $scope.getInboxMsgs();
        }, function (res) {
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.moveIntoInbox = function () {
        Service.moveIntoInbox($scope.moveToInboxObj).then(function (res) {
            swal('Success', res.data.response, 'success');
            $scope.getDataIntoLabel();
        }, function (res) {
            swal('Error', res.data.message, 'error');
        });
    };

    //*******************************************Move Message*****************************************//

    //***********************************************NEW************************************************//

    $rootScope.$on('getInbox', function () {
        $scope.getInboxMsgs();
    });

    /************************** Group APIs for add groups and move users************************************/

    $scope.createDeafaultGroupData = {};
    $scope.createDefaultGroup = function () {
        if ($scope.createDeafaultGroupData.disabled) {
            return false;
        }
        $scope.createDeafaultGroupData.disabled = true;
        Service.createDefaultGroup($scope.createDeafaultGroupData).then(function (res) {
            $("#addNewGroup").modal('hide');
            $scope.createDeafaultGroupData.disabled = false;
            $scope.getMessageGroups();
        }, function (res) {
            swal('Error', res.data.message, 'error');
            $scope.createDeafaultGroupData.disabled = false;
        })
    };

    $scope.moveUserGroupData = {};
    $scope.moveUserGroupData.users = [];
    $scope.moveUserGroup = function () {
        if ($scope.moveUserGroupData.disabled) {
            return false;
        }
        $scope.moveUserGroupData.disabled = true;
        $scope.moveUserGroupData.oldGroupId = $state.params.groupId;
        Service.moveUserGroup($scope.moveUserGroupData).then(function (res) {
            $scope.moveUserGroupData.disabled = false;
            $("#moveUser").modal("hide");
            setTimeout(function () {
                $state.reload();
            }, 500);
        }, function (res) {
            swal('Error', res.data.message, 'error');
            $scope.moveUserGroupData.disabled = false;
        });
    };

    $scope.groupcheckAllChange = function () {
        if ($('#groupcheckall').prop('checked') && $scope.messageMememberData.length) {
            for (var i = 0; i < $scope.messageMememberData.length; i++) {
                $scope.moveUserGroupData.users[i] = $scope.messageMememberData[i].id;
            }
        } else {
            $scope.moveUserGroupData.users = [];
        }
    };

    $scope.reloadCurrentState = function () {
        $scope.messageSearch = false;
        $scope.searchBarData.search_text = "";
    }

}]);
