angular.module('ecampus').controller('NewsFeedController', ['$scope', 'Service', '$state', '$stateParams', '$state', '$rootScope', 'Storage', function ($scope, Service, $state, $stateParams, $state, $rootScope, Storage) {

    $rootScope.$on('news_feeds', function () {
        $scope.getNewsFeed();
    });

    $scope.feedUploadImg = {};
    $scope.feedUploadImg.data = [];
    $scope.postNewsFeedImage = function () {
        var fd = new FormData();
        var file = $scope.uploadFile;
        if (file.size > $rootScope.maxAttachmentSize) {
            $.alert('Max image size 10 MB');
            return;
        }
        fd.append('file', file);
        $scope.feedUploadImg.show = true;
        var xhr = new XMLHttpRequest();
        xhr.upload.onprogress = function (e) {
            $scope.$apply(function () {
                if (e.lengthComputable) {
                    $scope.feedUploadImg.per = Math.round(e.loaded / e.total * 100);
                    $scope.feedUploadImg.text = $scope.feedUploadImg.per + '%';
                    if ($scope.feedUploadImg.per >= 100) {
                        $scope.feedUploadImg.show = false;
                    }
                }
            });
        };

        xhr.upload.onload = function (e) {
            $scope.$apply(function () {
                xhr.onreadystatechange = function () {
                    if (xhr.readyState == 4 && xhr.status == 200) {
                        var response = JSON.parse(xhr.responseText)
                        $scope.feedUploadImg.data.push(response.response);
                        $scope.$apply();
                    }
                }
            });
        }

        xhr.open('POST', $rootScope.base_url + '/api/upload-feed-image', true);
        xhr.setRequestHeader('Authorization', 'Bearer ' + Storage.get("ecampus_auth", true).token);
        xhr.send(fd);
    };

    $scope.removeFeedImg = function (index) {
        $scope.feedUploadImg.data.splice(index, 1);
    };

    $scope.feedUploadAttach = {};
    $scope.feedUploadAttach.data = [];
    $scope.postNewsfeedAttechedment = function () {
        var fd = new FormData();
        var file = $scope.uploadFile;
        if (file.size > $rootScope.maxAttachmentSize) {
            $.alert('Max file size 10 MB');
            return;
        }
        fd.append('file', file);
        $scope.feedUploadAttach.show = true;
        var xhr = new XMLHttpRequest();
        xhr.upload.onprogress = function (e) {
            $scope.$apply(function () {
                if (e.lengthComputable) {
                    $scope.feedUploadAttach.per = Math.round(e.loaded / e.total * 100);
                    $scope.feedUploadAttach.text = $scope.feedUploadAttach.per + '%';
                    if ($scope.feedUploadAttach.per >= 100) {
                        $scope.feedUploadAttach.show = false;
                    }
                }
            });
        };

        xhr.upload.onload = function (e) {
            $scope.$apply(function () {
                xhr.onreadystatechange = function () {
                    if (xhr.readyState == 4 && xhr.status == 200) {
                        var response = JSON.parse(xhr.responseText);
                        $scope.feedUploadAttach.data.push(response.response);
                        $scope.$apply();
                    }
                }
            });
        };

        xhr.open('POST', $rootScope.base_url + '/api/upload-feed-attachments', true);
        xhr.setRequestHeader('Authorization', 'Bearer ' + Storage.get("ecampus_auth", true).token);
        xhr.send(fd);
    };

    $scope.removeFeedAttach = function (index) {
        $scope.feedUploadAttach.data.splice(index, 1);
    };

    $scope.allModerators = [];
    $scope.getModeratorsList = function () {
        Service.getModerator().then(function (res) {
            $scope.allModerators = res.data.response;
            $scope.isModerator = res.data.moderator;
        }, function (res) {
        });
    };

    $scope.newsFeedData = {};
    $rootScope.newsFeedData = {};
    $scope.newsFeedData.images = [];
    // $scope.newsFeedData.content = "";
    $scope.newsFeedData.attachments = [];
    $scope.postNewsFeedSubmit = function () {
        $scope.newsFeedData.images = [];
        $scope.newsFeedData.attachments = [];
        if ($scope.newsFeedData.disabled) {
            return false;
        }
        angular.forEach($scope.feedUploadImg.data, function (val, key) {
            $scope.newsFeedData.images.push(val.imageName);
        });
        angular.forEach($scope.feedUploadAttach.data, function (val, key) {
            $scope.newsFeedData.attachments.push(val.fileName);
        });
        if ($rootScope.newsFeedData.content) {
            $scope.newsFeedData.content = $rootScope.newsFeedData.content;
        }
        $scope.newsFeedData.disabled = true;
        Service.postNewsFeed($scope.newsFeedData).then(function (res) {
            $scope.newsFeedData.disabled = false;
            angular.forEach($scope.feedUploadImg.data, function (val, key) {
                $scope.feedUploadImg.data.splice(val.imageName);
            });
            angular.forEach($scope.feedUploadAttach.data, function (val, key) {
                $scope.feedUploadAttach.data.splice(val.fileName);
            });
            $scope.newsFeedData.content = "";
            swal('Success', res.data.response, 'success');
            setTimeout(function () {
                $('#postNewsModal').modal('hide');
            }, 500);
            $scope.getAllNewsFeeds();
            $scope.getOwnPosts();
            $scope.getNewsFeed();
        }, function (res) {
            $scope.newsFeedData.disabled = false;
            swal('Error', res.data.response, 'error');
        })
    };

    $scope.getNewsFeedPosts = [];
    $scope.getNewsFeed = function () {
        Service.getNewsFeed({'search': $scope.getFeedData.search}).then(function (res) {
            $scope.getNewsFeedPosts = res.data.response.data;
            $scope.countOfPendingPost = res.data.response.pendingCount;
            $scope.countOfArchivedPost = res.data.response.archivedCount;
        }, function (res) {
            $scope.getNewsFeedPosts = [];
        });
    };

    $scope.approvedPostData = {};
    $scope.approvedPostSubmit = function (postid) {
        $scope.approvedPostData.feedId = postid;
        Service.approvedPost($scope.approvedPostData).then(function (res) {
            // swal('Success', res.data.response, 'success').then(function () {
            //     $scope.getNewsFeed();
            //     $scope.getAllNewsFeeds();
            // }, function () {
            // });

            swal({
                title: 'Success',
                type: 'success',
                showCancelButton: false,
                showConfirmButton: false,
                timer: 2000
            })

            // swal('Success', res.data.response, 'success');
            $scope.getNewsFeed();
            $scope.getAllNewsFeeds();

        }, function (res) {
            swal('Error', res.data.response, 'error');
        })
    };

    $scope.confirmToApprove = function (postid) {
        swal({
            title: 'Are you sure?',
            type: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, approve!'
        }).then(function () {
            $scope.approvedPostSubmit(postid);
        })
    };

    $scope.declinePostData = {};
    $scope.declinePostSubmit = function (postid) {
        $scope.declinePostData.feedId = postid;
        Service.declinedPost($scope.declinePostData).then(function (res) {
            $scope.getNewsFeed();
            swal('Success', res.data.response, 'success');
        }, function (res) {
            swal('Error', res.data.response, 'error');
        })
    };

    $scope.confirmToDecline = function (postid) {
        swal({
            title: 'Are you sure?',
            type: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, deline!'
        }).then(function () {
            $scope.declinePostSubmit(postid);
        })
    };

    $scope.archivedPostData = {};
    $scope.archivedPostSubmit = function (postid) {
        $scope.archivedPostData.feedId = postid;
        Service.archivedsPost($scope.archivedPostData).then(function (res) {
            swal('Success', res.data.response, 'success').then(function () {
                $scope.getNewsFeed();
            }, function () {
                $scope.getNewsFeed();
            });
        }, function (res) {
            swal('Error', res.data.response, 'error');
        })
    };

    $scope.confirmToArchived = function (postid) {
        swal({
            title: 'Are you sure?',
            type: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, archive!'
        }).then(function () {
            $scope.archivedPostSubmit(postid);
        })
    };


    $scope.getFeedData = {};
    $scope.getAllFeeds = [];
    $scope.getFeedData.totalItems = "";
    $scope.getFeedData.pageNo = 1;
    $scope.getFeedData.itemsPerPage = 10;
    $scope.getFeedData.limit = 10;
    $scope.setFeedPage = function (pageNo) {
        $scope.getFeedData.pageNo = pageNo;
    };

    $scope.getAllNewsFeeds = function (text) {
        $rootScope.newsFeedRendered = false;
        if (text) {
            $scope.getFeedData.filterBy = text;
        } else {
            $scope.getFeedData.filterBy = "";
        }
        Service.getAllFeed($scope.getFeedData).then(function (res) {
            $scope.getAllFeeds = [];
            setTimeout(function () {
                $scope.$apply(function () {
                    $scope.getAllFeeds = res.data.response.data;
                    $scope.getFeedData.totalItems = res.data.response.count;
                    resultLength = $scope.getFeedData.totalItems;
                    if (text != 'achievements') {
                        $('HTML, BODY').animate({scrollTop: 520}, 1000);
                    }
                });
            }, 100);
        }, function () {
            $scope.getAllFeeds = [];
        });
    };

    $scope.getOwnFeedData = {};
    $scope.getOwnPostsData = [];
    $scope.getOwnFeedData.totalItems = "";
    $scope.getOwnFeedData.pageNo = 1;
    $scope.getOwnFeedData.itemsPerPage = 20;
    $scope.setPage = function (pageNo) {
        $scope.getOwnFeedData.currentPage = pageNo;
    };

    $scope.getOwnPosts = function () {
        Service.getOwnPosts($scope.getOwnFeedData).then(function (res) {
            $scope.getOwnPostsData = res.data.response.data;
            $scope.getOwnFeedData.totalItems = res.data.response.count;
            resultLength = $scope.getOwnFeedData.totalItems;
        }, function (res) {
            $scope.getOwnPostsData = [];
        });
    };

    $scope.feedCommentData = {};
    $scope.addCommentsOnPost = function (obj) {
        if ($scope.feedCommentData.disabled) {
            return false;
        }
        $scope.feedCommentData.disabled = true;
        $scope.feedCommentData.feedId = obj.id;
        $scope.feedCommentData.comment = obj.comment;
        Service.addCommentsOnPost($scope.feedCommentData).then(function (res) {
            obj.comment = '';
            obj.comments = res.data.comments;
            //$scope.getNewsFeed();
            //$scope.getAllNewsFeeds();
            //$scope.getOwnPosts();
            $scope.feedCommentData.disabled = false;
        }, function () {
            $scope.feedCommentData.disabled = false;
        });
    };

    $scope.deleteOwnPostData = [];
    $scope.deleteOwnPost = function (feedId) {
        Service.deleteOwnPost(feedId).then(function (res) {
            $scope.deleteOwnPostData = res.data.response;
            $scope.getOwnPosts();
            swal(
                'Deleted!',
                'Your post has been deleted.',
                'success'
            )
        }, function (res) {
            $scope.deleteOwnPostData = [];
        })
    };

    $scope.confirmDelete = function (feedId) {
        swal({
            title: 'Are you sure?',
            text: "You won't be able to see this post!",
            type: 'question',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, delete it!'
        }).then(function () {
            $scope.deleteOwnPost(feedId);
        })
    };

    $scope.getUnapprovedPost = function () {
        Service.getUnapprovedPost({}).then(function (res) {
            $scope.getNewsFeedPosts = res.data.response.data;
        }, function (res) {
            $scope.getNewsFeedPosts = [];
        });
    };

    $scope.confirmToApproveAdmin = function (a, b) {
        Service.postActionAdmin({
            'feedId': a,
            'status': b
        }).then(function (res) {
            swal('Success!', 'Done', 'success');
            $scope.getUnapprovedPost();
        }, function (res) {
            swal('Error', res.data.message, 'error');
        });
    };

    $scope.confirmDeleteAdmin = function (id) {
        swal({
            title: 'Are you sure?',
            type: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, Delete!'
        }).then(function () {
            $scope.deletePostAdmin(id);
        })
    };

    $scope.deletePostAdmin = function (id) {
        Service.postDeleteAdmin({
            'id': id
        }).then(function (res) {
            swal('Success', res.response, 'success');
            $scope.getAllNewsFeeds();
            $scope.getNewsFeed()
        }, function (res) {
            swal('Error', res.data.message, 'error');
        });
    }

}]);



