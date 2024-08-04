---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Text Elements
0 ... m ... (n-k) ... n
m = middle point
k = range
x = target
 ^bW42eYKJ

Create a window to find the correct boundaries,
we want to balance the distance between the left
boundary and the target and the right boundary and 
the target ^jKT83A8q

goal => A[mid] _ _ _ x _ _ _ A[mid+k] ^Mp61SLrR

Find the correct left boundary that is closest
to target ^CpkqDxRi


left boundary will always be less than n-k, so
we only need to perform binary search from
0 to n-k to find the left boundary ^9JJnBDpW

x - A[mid]: distance between the target and left boundary
A[mid + k] - x: distance between the target and the right boundary
 ^XloSOVDn

%%
# Drawing
```json
{
	"type": "excalidraw",
	"version": 2,
	"source": "https://github.com/zsviczian/obsidian-excalidraw-plugin/releases/tag/1.9.8",
	"elements": [
		{
			"type": "text",
			"version": 404,
			"versionNonce": 1153787067,
			"isDeleted": false,
			"id": "bW42eYKJ",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -77.1324598754781,
			"y": -308.12773948100767,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 187.4398956298828,
			"height": 125,
			"seed": 641690715,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402278340,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "0 ... m ... (n-k) ... n\nm = middle point\nk = range\nx = target\n",
			"rawText": "0 ... m ... (n-k) ... n\nm = middle point\nk = range\nx = target\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "0 ... m ... (n-k) ... n\nm = middle point\nk = range\nx = target\n",
			"lineHeight": 1.25,
			"baseline": 118
		},
		{
			"type": "rectangle",
			"version": 326,
			"versionNonce": 1614583925,
			"isDeleted": false,
			"id": "fkCO0G_hOpoO-MhEaCNqj",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -82.40514065144288,
			"y": -311.0277033131348,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 154.68359375,
			"height": 28.054687499999993,
			"seed": 1231158139,
			"groupIds": [],
			"frameId": null,
			"roundness": {
				"type": 3
			},
			"boundElements": [],
			"updated": 1690402278340,
			"link": null,
			"locked": false
		},
		{
			"type": "text",
			"version": 473,
			"versionNonce": 1104090459,
			"isDeleted": false,
			"id": "jKT83A8q",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -80.23107324624993,
			"y": -70.88786080528308,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 535.379638671875,
			"height": 100,
			"seed": 310966005,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402278340,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Create a window to find the correct boundaries,\nwe want to balance the distance between the left\nboundary and the target and the right boundary and \nthe target",
			"rawText": "Create a window to find the correct boundaries,\nwe want to balance the distance between the left\nboundary and the target and the right boundary and \nthe target",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Create a window to find the correct boundaries,\nwe want to balance the distance between the left\nboundary and the target and the right boundary and \nthe target",
			"lineHeight": 1.25,
			"baseline": 93
		},
		{
			"type": "text",
			"version": 246,
			"versionNonce": 1448853973,
			"isDeleted": false,
			"id": "Mp61SLrR",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -80.4202506433582,
			"y": 49.62692058153988,
			"strokeColor": "#e03131",
			"backgroundColor": "transparent",
			"width": 417.0597839355469,
			"height": 25,
			"seed": 317890773,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402278340,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "goal => A[mid] _ _ _ x _ _ _ A[mid+k]",
			"rawText": "goal => A[mid] _ _ _ x _ _ _ A[mid+k]",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "goal => A[mid] _ _ _ x _ _ _ A[mid+k]",
			"lineHeight": 1.25,
			"baseline": 18
		},
		{
			"type": "text",
			"version": 286,
			"versionNonce": 530166267,
			"isDeleted": false,
			"id": "CpkqDxRi",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -82.08018026593453,
			"y": -372.1635344441746,
			"strokeColor": "#1e1e1e",
			"backgroundColor": "transparent",
			"width": 462.5595703125,
			"height": 50,
			"seed": 2052461909,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402278340,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "Find the correct left boundary that is closest\nto target",
			"rawText": "Find the correct left boundary that is closest\nto target",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "Find the correct left boundary that is closest\nto target",
			"lineHeight": 1.25,
			"baseline": 43
		},
		{
			"type": "text",
			"version": 193,
			"versionNonce": 93241141,
			"isDeleted": false,
			"id": "9JJnBDpW",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -84.32926800807343,
			"y": -201.69577599271418,
			"strokeColor": "#f08c00",
			"backgroundColor": "transparent",
			"width": 450.55963134765625,
			"height": 100,
			"seed": 855576949,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402278340,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "\nleft boundary will always be less than n-k, so\nwe only need to perform binary search from\n0 to n-k to find the left boundary",
			"rawText": "\nleft boundary will always be less than n-k, so\nwe only need to perform binary search from\n0 to n-k to find the left boundary",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "\nleft boundary will always be less than n-k, so\nwe only need to perform binary search from\n0 to n-k to find the left boundary",
			"lineHeight": 1.25,
			"baseline": 93
		},
		{
			"type": "text",
			"version": 163,
			"versionNonce": 571973403,
			"isDeleted": false,
			"id": "XloSOVDn",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": -71.30232736441752,
			"y": 111.47917141940059,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 677.8994140625,
			"height": 75,
			"seed": 140224315,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402532158,
			"link": null,
			"locked": false,
			"fontSize": 20,
			"fontFamily": 1,
			"text": "x - A[mid]: distance between the target and left boundary\nA[mid + k] - x: distance between the target and the right boundary\n",
			"rawText": "x - A[mid]: distance between the target and left boundary\nA[mid + k] - x: distance between the target and the right boundary\n",
			"textAlign": "left",
			"verticalAlign": "top",
			"containerId": null,
			"originalText": "x - A[mid]: distance between the target and left boundary\nA[mid + k] - x: distance between the target and the right boundary\n",
			"lineHeight": 1.25,
			"baseline": 68
		},
		{
			"type": "freedraw",
			"version": 6,
			"versionNonce": 1430682869,
			"isDeleted": true,
			"id": "5xvMDly92gpmmBdUr56NN",
			"fillStyle": "hachure",
			"strokeWidth": 1,
			"strokeStyle": "solid",
			"roughness": 1,
			"opacity": 100,
			"angle": 0,
			"x": 205.29338219582365,
			"y": -475.5607844273655,
			"strokeColor": "#1971c2",
			"backgroundColor": "transparent",
			"width": 0.303930775964659,
			"height": 0,
			"seed": 286935509,
			"groupIds": [],
			"frameId": null,
			"roundness": null,
			"boundElements": [],
			"updated": 1690402587550,
			"link": null,
			"locked": false,
			"points": [
				[
					0,
					0
				],
				[
					-0.303930775964659,
					0
				],
				[
					0,
					0
				]
			],
			"lastCommittedPoint": null,
			"simulatePressure": true,
			"pressures": []
		}
	],
	"appState": {
		"theme": "light",
		"viewBackgroundColor": "#ffffff",
		"currentItemStrokeColor": "#1971c2",
		"currentItemBackgroundColor": "transparent",
		"currentItemFillStyle": "hachure",
		"currentItemStrokeWidth": 1,
		"currentItemStrokeStyle": "solid",
		"currentItemRoughness": 1,
		"currentItemOpacity": 100,
		"currentItemFontFamily": 1,
		"currentItemFontSize": 20,
		"currentItemTextAlign": "left",
		"currentItemStartArrowhead": null,
		"currentItemEndArrowhead": "arrow",
		"scrollX": 1161.2314688272832,
		"scrollY": 1327.2262855945878,
		"zoom": {
			"value": 0.2196750613024872
		},
		"currentItemRoundness": "round",
		"gridSize": null,
		"currentStrokeOptions": null,
		"previousGridSize": null
	},
	"files": {}
}
```
%%