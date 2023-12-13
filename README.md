-using LB2.API.Models;
using LB2.API.Services.Interfaces;
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace LB2.UI
{
    public partial class FreightReceivingDeliveryForm : Form
    {
        private CommonParcelModel _commonParcelModel;
        private IClientCardService _clientCardService;
        private ClientCard _clientCard;
        public FreightReceivingDeliveryForm(CommonParcelModel commonParcelModel, IClientCardService clientCardService, ClientCard clientCard)
        {
            InitializeComponent();
            _commonParcelModel = commonParcelModel;
            _clientCardService = clientCardService;
            _clientCard = clientCard;
        }

        private void button1_Click(object sender, EventArgs e)
        {
            var receiverPhoneNumber = textBox1.Text;
            var receiverAddress = textBox2.Text;
            var specialPacking = checkBox1.Checked;
            var numberOfLoaders = textBox3.Text;
            var result = _clientCardService.RegisterFreightReceivingDelivery(_clientCard, new API.Models.Receiving.FreightReceivingDelivery(_commonParcelModel.OperationDate,
                _commonParcelModel.Weight, _commonParcelModel.SenderName, _commonParcelModel.SenderPayment, _commonParcelModel.ReceiverName,
                receiverPhoneNumber, receiverAddress, specialPacking, int.Parse(numberOfLoaders)), false);
            MessageBox.Show("Вартість:" + result.ToString());
            this.Close();
        }
    }
}
