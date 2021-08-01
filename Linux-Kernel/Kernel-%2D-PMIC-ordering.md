# drivers/spmi/spmi.c
- for dev_set_name(&sdev->dev, "spmi%d-%02x", ctrl->nr, sdev->usid);
  - nr: controller identifier
  - usid: slave id
```
/**
 * spmi_device_add() - add a device previously constructed via spmi_device_alloc()
 * @sdev:	spmi_device to be added
 */
int spmi_device_add(struct spmi_device *sdev)
{
	struct spmi_controller *ctrl = sdev->ctrl;
	int err;

	dev_set_name(&sdev->dev, "spmi%d-%02x", ctrl->nr, sdev->usid);

	err = device_add(&sdev->dev);
	if (err < 0) {
		dev_err(&sdev->dev, "Can't add %s, status %d\n",
			dev_name(&sdev->dev), err);
		goto err_device_add;
	}

	dev_dbg(&sdev->dev, "device %s registered\n", dev_name(&sdev->dev));

err_device_add:
	return err;
}
EXPORT_SYMBOL_GPL(spmi_device_add);
```