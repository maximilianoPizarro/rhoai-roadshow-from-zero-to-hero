# 🧹 Cleanup and Deprovision the Environment

After completing the RHAIIS module, you should cleanup and restore the environment to its default state so that you can continue with other modules or free up resources.

## Overview

The cleanup process involves:
- Restoring default model deployments in the `llama-serving` namespace
- Verifying that the environment is ready for other activities
- Optionally removing any custom deployments you created during this module

## Step 1: Access OpenShift Console

1. Navigate to the OpenShift AI Console:
   <a href="https://console-openshift-console.apps.<CLUSTER_DOMAIN>" target="_blank">https://console-openshift-console.apps.<CLUSTER_DOMAIN></a>

2. Authenticate with your credentials

## Step 2: Restore Default Model Deployments

If you stopped the default models during the RHAIIS exercises, you need to restore them:

1. Navigate to **Models** > **Model deployments** in the Red Hat OpenShift AI Web Console

2. **Start** both default model deployments:
   - **Llama3** (start this one first)
   - **DeepSeek** (start this one second)

   ![Model Serving Stop/Start](../images/model-serving-stop-start.png)

⚠️ **Important:** The **order** matters for correct startup due to GPU memory constraints:
- Llama3 uses `gpu_memory_utilization=0.5`
- DeepSeek uses `gpu_memory_utilization=0.8`
- Starting Llama3 first ensures proper GPU memory allocation

## Step 3: Verify Default Models are Running

You can verify the models are running using the OpenShift CLI:

```bash
oc login --server=https://api.<CLUSTER_DOMAIN>:6443 -u admin -p password
oc get pods -n llama-serving
```

You should see both model deployment pods in `Running` state:

```
NAME                                                READY   STATUS    RESTARTS   AGE
llama3-2-3b-predictor-xxxxx                        2/2     Running   0          XmXs
sno-deepseek-qwen3-vllm-predictor-xxxxx            2/2     Running   0          XmXs
```

![Default Models](../images/default-models.png)

## Step 4: Optional - Remove Custom Deployments

If you deployed any custom models during this module (e.g., `granite-3.1-2b-instruct`), you can remove them:

1. Navigate to **Models** > **Model deployments**
2. Find your custom deployment
3. Click the **⋮** menu and select **Delete**
4. Confirm the deletion

This will free up GPU resources for other activities.

## Step 5: Verify Environment is Ready

✅ Check that default models are running  
✅ Verify GPU resources are available  
✅ Confirm no custom deployments are consuming resources unnecessarily  

🎉 **Congratulations!** Your environment is now cleaned up and ready for other modules or activities.

---

## Continue Your Journey

✅ **Next**: [Resources](6-resources/README) - Source code, installation methods, and more  
👥 **About**: [About the Team](5-about-the-team/README) - Thank you for participating!

---

**Return to**: [Main Page](/)
