{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "DenyRunInstanceWithoutTribeTag",
        "Effect": "Deny",
        "Action": [
          "ec2:RunInstances"
        ],
        "Resource": [
          "arn:aws:ec2:*:*:instance/*"
        ],
        "Condition": {
          "StringNotLike": {
            "aws:RequestTag/tribe": [
              "?*"
            ]
          }
        }
      }
    ]
  }


/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "ec2:CreateVolume"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:volume/*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "ec2:CreateNatGateway"
      ],
      "Resource": [
        "arn:aws:ec2:*:*:natgateway/*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyRedShiftWithoutTribeTag",
      "Effect": "Deny",
      "Action": [
        "redshift:CreateCluster"
      ],
      "Resource": [
        "arn:aws:redshift:*:*:cluster:*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenysgWithoutTribeTag",
      "Effect": "Deny",
      "Action": [
        "sagemaker:CreateNotebookInstance"
      ],
      "Resource": [
        "arn:aws:sagemaker:*:*:notebook-instance/*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": "?*"
        }
      }
    }
  ]
}

/*----------------------------------------------*/
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "glue:CreateCrawler",
        "glue:CreateJob",
        "glue:CreateTrigger",
        "glue:CreateWorkflow",
        "glue:CreateDevEndpoint",
        "glue:CreateMLTransform"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}


/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Deny",
      "Action": "cognito-idp:CreateUserPool",
      "Resource": "*",
      "Condition": {
        "StringNotEquals": {
          "aws:RequestTag/tribe": "?*"
        }
      }
    }
  ]
}

/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "kinesisanalytics:CreateApplication"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "ecs:CreateCluster",
        "ecs:CreateTaskSet"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*----------------------------------------------*/


{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "ecr:CreateRepository"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*----------------------------------------------*/

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "ses:CreateConfigurationSet",
        "ses:CreateReceiptRule",
        "ses:CreateReceiptRuleSet"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# CloudWatch Logs
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "logs:CreateLogGroup"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}


/*--------------------------------------------*/

# X-RAY
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "xray:CreateGroup",
        "cloudformation:CreateStack"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/
# EMR

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "emr-containers:CreateVirtualCluster",
        "emr-containers:CreateManagedEndpoint"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# ELASTIC FILE SYSTEM

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "elasticfilesystem:CreateFileSystem"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    },
    {
      "Sid": "Statement2",
      "Effect": "Deny",
      "Action": [
        "elasticfilesystem:CreateAccessPoint"
      ],
      "Resource": [
        "arn:aws:elasticfilesystem:*:*:file-system/*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# WAF 

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "waf:CreateRateBasedRule",
        "waf:CreateRule",
        "waf:CreateRuleGroup",
        //"waf:CreateWebACL" 
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# KMS

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "kms:CreateKey"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# SECRET MANAGER

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "secretsmanager:CreateSecret"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# BACKUP

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "backup:CreateBackupPlan"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# SNS (Amazon Simple Notification Service)

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "sns:CreateTopic"
      ],
      "Resource": [
        "arn:aws:sns:*:*:*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# CODE COMMIT

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "codecommit:CreateRepository"
      ],
      "Resource": [
        "arn:aws:codecommit:*:*:*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# RDS

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "rds:CreateDBCluster",
        "rds:CreateDBInstance"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# elasticache

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "elasticache:CreateCacheCluster"
      ],
      "Resource": [
        "arn:aws:elasticache:*:*:parametergroup:*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

# Transfer Family sftp

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "transfer:CreateServer"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}






{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Deny",
			"Action": [
				"rekognition:CreateCollection",
				"rekognition:CreateProjectVersion",
				"rekognition:CreateStreamProcessor"
			],
			"Resource": [
				"*"
			],
			"Condition": {
				"StringNotLike": {
					"aws:RequestTag/tribe": [
						"?*"
					]
				}
			}
		}
	]
}

/*--------------------------------------------*/


{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Effect": "Deny",
      "Action": [
        "quicksight:CreateAccountCustomization",
        "quicksight:CreateDashboard",
        "quicksight:CreateDataSet",
        "quicksight:CreateDataSource",
        "quicksight:CreateNamespace",
        "quicksight:CreateTemplate",
        "quicksight:CreateTheme"
      ],
      "Resource": [
        "*"
      ],
      "Condition": {
        "StringNotLike": {
          "aws:RequestTag/tribe": [
            "?*"
          ]
        }
      }
    }
  ]
}

/*--------------------------------------------*/

{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Deny",
			"Action": [
				"config:Put*"
			],
			"Resource": [
				"*"
			],
			"Condition": {
				"StringNotLike": {
					"aws:RequestTag/tribe": [
						"?*"
					]
				}
			}
		}
	]
}   

/*--------------------------------------------*/

{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Deny",
			"Action": [
				"glacier:CreateVault"
			],
			"Resource": [
				"arn:aws:glacier:*:*:vaults/*"
			],
			"Condition": {
				"StringNotLike": {
					"aws:RequestTag/tribe": [
						"?*"
					]
				}
			}
		}
	]
}

/*--------------------------------------------*/

{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "Statement1",
			"Effect": "Deny",
			"Action": [
				"amplify:CreateApp"
			],
			"Resource": [
				"*"
			],
			"Condition": {
				"StringNotLike": {
					"aws:RequestTag/tribe": [
						"?*"
					]
				}
			}
		}
	]
}   

/*--------------------------------------------*/


/*--------------------------------------------*/



-----------------

