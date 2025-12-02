---
created: 2024-05-12 19:50
modified: 2025-06-15T18:41:09-04:00

---
tags:: [[aws]] [[s3]]
![[2024-05-12.excalidraw]]

**(client-side) User sends request to server to get pre-signedUrl**
``` ts
const handleFileInput = useCallback((input: HTMLInputElement) => {
  return async (event: Event) => {
    event.preventDefault();
    const file: File | null | undefined = input.files?.item(0);
    if (!file) return;
    const { getTweetImgPresignedUrl } = await graphqlClient.request(
      getTweetImgPresignedUrlQuery,
      {
        imgName: file.name,
        imgType: file.type,
      },
    );
    if (getTweetImgPresignedUrl) {
      const url = new URL(getTweetImgPresignedUrl);
      await fetch(url, {
        method: "PUT",
        body: file,
        headers: {
          "Content-Type": file.type,
        },
      });
      setImgUrl(url.origin + url.pathname);
    }
  };
}, []);

// Upload image callback function
const handleImageUpload = useCallback(() => {
  const input = document.createElement("input");
  input.setAttribute("type", "file");
  input.setAttribute("accept", "images/*");
  input.addEventListener("change", handleFileInput(input));
  input.click();
}, [handleFileInput]);

// <BsImage onClick={handleImageUpload} />
```

 **(server-side) Validate request and generate pre-signed url**
1. Install dependencies
	[@aws-sdk/client-s3 - npm](https://www.npmjs.com/package/@aws-sdk/client-s3)
	[@aws-sdk/s3-request-presigner - npm](https://www.npmjs.com/package/@aws-sdk/s3-request-presigner)
	[dotenv - npm](https://www.npmjs.com/package/dotenv)

2. load env variables
``` ts
import * as dotenv from "dotenv";
const env = dotenv.config();
```
3. set env variables in `.env`
```ts
AWS_DEFAULT_REGION=us-east-1
AWS_ACCESS_KEY_ID=example_key_id
AWS_SECRET_ACCESS_KEY=example_aws_secret_access_key
S3_BUCKET_NAME=twitter-fullstack
```
4. Initiate S3 client with configuration (e.g. credentials, region).
``` ts
import { S3Client, PutObjectCommand } from "@aws-sdk/client-s3";
import { getSignedUrl } from "@aws-sdk/s3-request-presigner";


const s3Client = new S3Client({
	region: process.env.AWS_DEFAULT_REGION,
});
```
5. Generate the presignedURL
``` ts
const queries = {
	// ... other queries
	getTweetImgPresignedUrl: async (
	  parent: any,
	  { ImgName, ImgType }: { ImgName: string; ImgType: string },
	  ctx: GraphQLContext
	) => {
	  // Check if the user is authorized
	  if (!ctx.user || !ctx.user.id)
	    throw new Error("You are not authorized to make this tweet");

	  // Define allowed image types
	  const allowedImgTypes = [
	    "image/jpeg",
	    "image/jpg",
	    "image/webp",
	    "image/png",
	  ];

	  // Check if the provided image type is allowed
	  if (!allowedImgTypes.includes(ImgType))
	    throw new Error("Image type not supported");

	  // Create the PutObjectCommand with the specified bucket and key
	  const putObjectCommand = new PutObjectCommand({
	    Bucket: "dezire-twitter-clone-dev",
	    Key: `uploads/${ctx.user.id}/${
	      ImgName.split(".")[0]
	    }-${Date.now().toString()}.${ImgType.split("/")[1]}`,
	  });

	  // Generate a signed URL for the putObjectCommand
	  const signedUrl = await getSignedUrl(s3Client, putObjectCommand, {
	    expiresIn: 300,
	  });

	  // Return the signed URL
	  return signedUrl;
	},
};
```

[[How to set up AWS S3 bucket to store files]]
**Sources**
[Uploading Photos to Amazon S3 from a Browser - AWS SDK for JavaScript](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/s3-example-photo-album.html)

[Server-code](https://github1s.com/debarkamondal/twitter-clone-backend/commit/c74a7bbbf35afa7690a08a67ed5da6046b845f47)
[Client-code](https://github1s.com/debarkamondal/twitter-clone-frontend/commit/018cff3d047acacd2bdb6ede7b711ec1a337fd0a)
